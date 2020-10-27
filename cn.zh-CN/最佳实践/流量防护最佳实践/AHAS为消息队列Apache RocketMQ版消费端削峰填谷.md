---
keyword: [RocketMQ, 削峰填谷, 消息队列Kafka Consumer]
---

# AHAS为消息队列Apache RocketMQ版消费端削峰填谷

AHAS应用防护功能与消息队列RocketMQ组合，可以让MQ消费端负载保持在消息处理水位之下，同时尽可能处理更多消息，达到削峰填谷的效果。本文以AHAS应用防护的匀速处理请求的能力为例，说明如何对RocketMQ消费端进行限流。

## 背景信息

在消息队列RocketMQ中，消费者消费消息时，很可能出现因消息发送量突增而消费者来不及处理的情况，导致消费方负载过高，进而导致影响系统稳定性。

在实际场景中，消息的到来具有瞬时性、不规律性，导致系统可能出现空闲资源。利用AHAS应用防护的匀速处理请求的能力，可以把超过消费端处理能力的消息（图中黄色部分）均摊到后面系统空闲时去处理，让系统负载处在一个稳定的水位，同时尽可能地处理更多消息，起到削峰填谷的作用。

![削峰填谷](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/4373698951/p132378.png)

AHAS应用防护在削峰填谷的场景时，以固定的间隔时间让请求通过，以稳定的速度逐步处理这些请求，避免流量突刺造成系统负载过高。同时堆积的请求将会排队，逐步进行处理；当请求排队预计超过最大超时时长的时候则直接拒绝，而不是拒绝全部请求。

例如，在RocketMQ的场景下，配置匀速模式下请求QPS为8，则每200 ms处理一条消息，多余的处理任务将排队；同时配置超时时间为8秒，预计的排队时长超过8秒的处理任务将会被直接拒绝。

![原理图](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/4373698951/p132379.png)

## 前提条件

-   已在消息队列RocketMQ中发送和订阅消息，请参见[主账号快速入门](https://help.aliyun.com/document_detail/34411.html)和[子账号快速入门](https://help.aliyun.com/document_detail/96402.html)。
-   已开通AHAS，请参见[开通 AHAS](/cn.zh-CN/快速入门/开通 AHAS.md)。

## 步骤一：接入AHAS应用防护

下面将介绍如何快速在消息队列RocketMQ Consumer （消费端）接入和使用AHAS应用防护服务 。您可以下载[Demo工程](https://aliware-images.oss-cn-hangzhou.aliyuncs.com/ahas/ahas-sentinel-mq-demo.zip)来完成以下步骤。

1.  在Consumer的pom文件中引入AHAS应用防护（即Sentinel）依赖。

    ```
    <dependency>
        <groupId>com.alibaba.csp</groupId>
        <artifactId>ahas-sentinel-client</artifactId>
        <version>x.y.z</version>
    </dependency>
    ```

    **说明：** 请在[AHAS依赖仓库](https://search.maven.org/search?q=a:ahas-sentinel-client)查看依赖最新版本。

2.  定义资源。

    由于消息队列RocketMQ Consumer未提供相应拦截机制，而且每次收到都可能是批量的消息，因此用户需要在处理消息时手动定义资源。

    定义消息处理逻辑为消息被拒绝后会记录错误并触发重新投递，代码示例如下。

    ```
    private static Action handleMessage(Message message, String groupId, String topic) {
            Entry entry = null;
            try {
                // 定义资源。为了便于标识，资源名称定义为Group ID和Topic的组合。Group ID和Topic可以通过消息队列RocketMQ控制台获得。
                entry = SphU.entry("handleMqMessage:" + groupId + ":" + topic);
    
                // 业务真实的消息处理逻辑。
                System.out.println(System.currentTimeMillis() + " | handling message: " + message);
                return Action.CommitMessage;
            } catch (BlockException ex) {
                // 编写被流控的消息的处理逻辑。示例：记录错误或进行重试。
                System.err.println("Blocked, will retry later: " + message);
                // 会触发消息重新投递
                return Action.ReconsumeLater; 
            } finally {
                if (entry != null) {
                    entry.exit();
                }
            }
        }
    ```

    消费者订阅消息的逻辑示例如下。

    ```
    Consumer consumer = ONSFactory.createConsumer(properties);
    consumer.subscribe(topic, "*", (message, context) -> {
        return handleMessage(message);
    });
    consumer.start();
    ```

    关于消息队列RocketMQ如何订阅消息，请参见[消息队列RocketMQ文档](https://help.aliyun.com/document_detail/34411.html?#h2--5)。

3.  登录[AHAS控制台](https://ahas.console.aliyun.com)，获取AHAS启动参数。
    1.  在控制台最上方地域列表中，选择地域为**公网**。
    2.  在左侧导航栏选择**流量防护** \> **应用防护**，单击右上角**新应用接入**。
    3.  选择**SDK应用接入** \> **自定义埋点**页签，查看启动参数。

        启动参数示例如下。

        ```
        -Dproject.name=MqConsumerDemo -Dahas.license=<License>
        ```

        其中`MqConsumerDemo`表示应用名，可自定义；`<License>`表示您的授权证书，请修改为真实值。

4.  在Consumer中添加启动参数。
5.  启动Publisher开始发送消息，再启动Consumer开始接收消息。

    启动Publisher、Consumer后，本地IDE的**consol**区域开始打印消息发送日志、消息接收日志，通过查看日志判断消息发送情况。


## 步骤二：配置削峰填谷规则

将应用接入AHAS应用防护后，需要为其配置规则来实现削峰填谷。

1.  登录[AHAS控制台](https://ahas.console.aliyun.com)，在左侧导航栏选择**流量防护** \> **应用防护**。
2.  在应用防护页面单击目标应用资源卡片，进入该应用管理界面。
3.  在左侧导航栏选择**应用概览**，在目标接口的**操作**列中，单击**流控**，填写流控规则，并单击**新建**完成创建。详情请参见[配置流控规则](/cn.zh-CN/流量防护/应用防护/配置规则/配置流控规则.md)。
    -   **流控效果**：排队等待。
    -   **单机QPS阈值**：QPS，设置QPS阈值为10，代表每100 ms匀速通过一个请求。
    -   **超时时间**：2000 ms，超出此超时时间的请求将立即被拒绝，不会进入队列。
4.  通过消息队列RocketMQ Producer端向Consumer批量发送消息，查看流控效果。
    -   在Consumer控制台，通过观察消息头部的时间戳（如下所示），可以发现消息消费的速率是匀速的，大约每100毫秒消费一条消息。同时，不断有排队的处理任务完成，超出等待时长的处理请求直接被拒绝。

        ```
        1550732955137 | handling message: Hello MQ 2453
        1550732955236 | handling message: Hello MQ 9162
        1550732955338 | handling message: Hello MQ 4944
        1550732955438 | handling message: Hello MQ 5582
        1550732955538 | handling message: Hello MQ 4493
        1550732955637 | handling message: Hello MQ 3036
        1550732955738 | handling message: Hello MQ 1381
        1550732955834 | handling message: Hello MQ 1450
        1550732955937 | handling message: Hello MQ 5871
        ```

        **说明：** 在处理被拒绝请求的时候，需要根据业务需求，决定是否重新消费消息。

    -   在[AHAS控制台](https://ahas.console.aliyun.com)的应用详情页面，单击**监控详情**，查看消息处理的监控曲线。

        ![pg_sentinel_app_monitor.png](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/4373698951/p158129.png)

        如果没有使用匀速限流模式，该消息处理的监控曲线会如下图。

        如果不开启匀速模式，只会同时处理10条消息，其余的全部被拒绝。即使后面的时间系统资源充足，多余的请求也无法被处理，因而浪费了许多空闲资源。两种模式对比说明匀速模式下消息处理能力得到了更好的利用。

        ![pg_sentinel_app_monitor_vs.png](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/4373698951/p158130.png)


## 消息队列Kafka Consumer接入示例

与消息队列RocketMQ类似，消息队列Kafka Consumer也可通过类似方法接入和使用AHAS应用防护服务。

示例：在处理消息的逻辑处定义资源。

```
private static void handleMessage(ConsumerRecord<String, String> record, String groupId, String topic) {
    pool.submit(() -> {
        Entry entry = null;
        try {
            // 定义资源。为了便于标识，资源名称定义为Group ID和Topic的组合。Group ID和Topic可以通过MQ控制台获得。
            entry = SphU.entry("handleKafkaMessage:" + groupId + ":" + topic);

            // 业务的消息处理逻辑。
            System.out.printf("[%d] Receive new messages: %s%n", System.currentTimeMillis(), record.toString());
        } catch (BlockException ex) {
            // Blocked
            // 在处理请求被拒绝的情况时候，需要根据业务需求，决定是否重新消费消息。
             System.err.println("Blocked: " + record.toString());
        } finally {
            if (entry != null) {
                entry.exit();
            }
        }
    });
}
```

示例：消费者订阅消息的逻辑如下。

```
while (true) {
    try {
        ConsumerRecords<String, String> records = consumer.poll(1000);
        // 必须在下次poll之前消费完这些数据, 且总耗时不得超过SESSION_TIMEOUT_MS_CONFIG。
        // 建议开一个单独的线程池来消费消息，然后异步返回结果。
        for (ConsumerRecord<String, String> record : records) {
            handleMessage(record, groupId, topic);
        }
    } catch (Exception e) {
        try {
            Thread.sleep(1000);
        } catch (Throwable ignore) {
        }
        e.printStackTrace();
    }
}
```

## 相关文档

本文介绍的是AHAS应用防护服务的一个场景：请求匀速。AHAS应用防护服务还可以处理更复杂的各种情况。

-   流量控制：针对不同的调用关系，以不同的运行指标（如QPS、线程数、系统负载等）为基准，对资源调用进行流量控制，将随机的请求调整成合适的形状（请求匀速、Warm Up等）。
-   熔断降级：当调用链路中某个资源出现不稳定的情况，如平均响应时间增高、异常比例升高的时候，使对此资源的调用请求快速失败，避免影响其它的资源导致级联失败。
-   系统负载保护：从系统的维度提供保护。当系统负载较高的时候，提供保护机制，让系统的入口流量和系统的负载达到一个平衡，保证系统在能力范围之内处理最多的请求。

详情请参见[AHAS应用防护](/cn.zh-CN/流量防护/应用防护/应用防护概述.md)。

