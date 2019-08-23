# AHAS 为 MQ 消费端削峰填谷 {#concept_tdp_ly2_zgb .concept}

AHAS 应用流控降级功能与消息队列 RocketMQ 组合，让系统负载保持在消息处理水位之下，同时尽可能地处理更多消息，达到“削峰填谷”的效果。本文以 AHAS 应用流控降级的匀速处理请求的能力为例，说明如何对 RocketMQ 消费端进行限流。

## 背景信息 {#section_yjq_cfl_zgb .section}

在消息队列 RocketMQ 中，消费者消费消息时，很可能出现因消息发送量突增而消费者来不及处理的情况，导致消费方负载过高，进而导致影响系统稳定性。

在实际场景中，消息的到来具有瞬时性、不规律性，导致系统可能出现空闲资源。利用 AHAS 应用流控降级的匀速处理请求的能力，可以把超过消费端处理能力的消息（图中红色部分）均摊到后面系统空闲时去处理，让系统负载处在一个稳定的水位，同时尽可能地处理更多消息，起到削峰填谷的作用。

![](https://aliware-images.oss-cn-hangzhou.aliyuncs.com/ahas/dg_peak_filling.png)

AHAS 应用流控降级在削峰填谷的场景时，以固定的间隔时间让请求通过，以稳定的速度逐步处理这些请求，避免流量突刺造成系统负载过高。同时堆积的请求将会排队，逐步进行处理；当请求排队预计超过最大超时时长的时候则直接拒绝，而不是拒绝全部请求。

例如，在 RocketMQ 的场景下，配置匀速模式下请求 QPS 为 5，则每 200 ms 处理一条消息，多余的处理任务将排队；同时配置超时时间为 5 秒，预计的排队时长超过 5 秒的处理任务将会被直接拒绝。

![](https://aliware-images.oss-cn-hangzhou.aliyuncs.com/ahas/dg_waiting_example.png)

## 前提条件 {#section_3f3_5wo_ho9 .section}

-   已在消息队列 RocketMQ 中发送和订阅消息，参见[主账号快速入门](https://help.aliyun.com/document_detail/34411.html)和[子账号快速入门](https://help.aliyun.com/document_detail/96402.html)。
-   已开通 AHAS，参见[开通 AHAS](../../../../intl.zh-CN/准备工作/开通 AHAS.md#)。

## 步骤一：接入 AHAS 应用流控降级 {#section_rcj_snl_zgb .section}

下面将介绍如何快速在消息队列 RocketMQ Consumer （消费端）接入和使用 AHAS 流控降级服务 。您可以在下载[Demo 工程](https://aliware-images.oss-cn-hangzhou.aliyuncs.com/ahas/ahas-sentinel-mq-demo.zip)来完成以下步骤。

1.  在 Consumer 的 pom 文件中引入 AHAS 应用流控降级（即 Sentinel）依赖。

    ``` {#codeblock_8ms_0mx_beg}
    <dependency>
        <groupId>com.alibaba.csp</groupId>
        <artifactId>ahas-sentinel-client</artifactId>
        <version>x.y.z</version>
    </dependency>
    ```

    **说明：** 请在 [AHAS 依赖仓库](https://search.maven.org/search?q=a:ahas-sentinel-client)查看依赖最新版本。

2.  定义资源。

    由于消息队列 RocketMQ Consumer 未提供相应拦截机制，而且每次收到都可能是批量的消息，因此用户需要在处理消息时手动定义资源。

    定义消息处理逻辑为消息被拒绝后会记录错误并触发重新投递，代码示例如下：

    ``` {#codeblock_305_lqs_fxv}
    private static Action handleMessage(Message message, String groupId, String topic) {
            Entry entry = null;
            try {
                // 定义资源。为了便于标识，资源名称定义为 Group ID 和 Topic 的组合。Group ID 和 Topic 可以通过消息队列 RocketMQ 控制台获得。
                entry = SphU.entry("handleMqMessage:" + groupId + ":" + topic);
    
                // 业务真实的消息处理逻辑
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

    消费者订阅消息的逻辑示例如下：

    ``` {#codeblock_6rx_fdr_7y2}
    Consumer consumer = ONSFactory.createConsumer(properties);
    consumer.subscribe(topic, "*", (message, context) -> {
        return handleMessage(message);
    });
    consumer.start();
    ```

    关于消息队列 RocketMQ 如何订阅消息，请参考 [消息队列 RocketMQ 文档](https://help.aliyun.com/document_detail/34411.html?#h2--5)。

3.  登录 [AHAS 控制台](https://ahas.console.aliyun.com)，获取 AHAS 启动参数。
    1.  在控制台最上方地域列表中，选择地域为**公网**。
    2.  在左侧导航栏选择**流控降级** \> **应用流控**，单击右上角**新应用接入**。
    3.  选择**SDK 应用接入** \> **自定义埋点**页签，查看启动参数。

        示例如下：

        ``` {#codeblock_s4e_wwt_zy8}
        -Dproject.name=MqConsumerDemo -Dahas.license=<License>
        ```

        其中，`MqConsumerDemo` 表示应用名，可自定义；`<License>` 表示您的授权证书，请修改为真实值。

4.  在 Consumer 中添加启动参数。
5.  启动 Publisher 开始发送消息，再启动 Consumer 开始接收消息。

    启动 Publisher/Consumer 后，本地 IDE 的 **consol** 区域开始打印消息发送日志/消息接收日志，通过查看日志判断消息发送情况。

6.  在请求链路页面，在对应的请求链路的**操作**列中，单击**流控**，填写流控规则，并单击**新建**完成创建。

    -   **流控方式**：排队等待
    -   **阈值类型**：QPS，设置 QPS 阈值为 10，代表每 100ms 匀速通过一个请求。
    -   **超时时间**（ms）：2000，超出此超时时间的请求将立即被拒绝，不会进入队列。
    ![](https://aliware-images.oss-cn-hangzhou.aliyuncs.com/ahas/pg_sentinel_app_request_list.png)

7.  通过消息队列 RocketMQ Producer 端向 Consumer 批量发送消息，查看流控效果。
    -   在 Consumer 控制台，通过观察消息头部的时间戳（如下所示），可以发现消息消费的速率是匀速的，大约每 100 毫秒消费一条消息。同时，不断有排队的处理任务完成，超出等待时长的处理请求直接被拒绝。

        ``` {#codeblock_pax_k2l_f95}
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

    -   在 [AHAS 控制台](https://ahas.console.aliyun.com)的应用详情页面，单击**监控详情**，查看消息处理的监控曲线：

        ![](https://aliware-images.oss-cn-hangzhou.aliyuncs.com/ahas/pg_sentinel_app_monitor.png)

        如果没有使用匀速限流模式，该消息处理的监控曲线会类似于：

        ![](https://aliware-images.oss-cn-hangzhou.aliyuncs.com/ahas/pg_sentinel_app_monitor_vs.png)

        如果不开启匀速模式，只会同时处理 10 条消息，其余的全部被拒绝。即使后面的时间系统资源充足，多余的请求也无法被处理，因而浪费了许多空闲资源。两种模式对比说明匀速模式下消息处理能力得到了更好的利用。


## 步骤二：配置削峰填谷规则 {#section_9wy_m26_o5w .section}

将应用接入 AHAS 应用流控降级后，需要为其配置规则来实现削峰填谷。

1.  登录 [AHAS 控制台](https://ahas.console.aliyun.com)。
    1.  在左侧导航栏选择**流控降级**。

    2.  单击已接入应用的卡片，进入详情页面。

    3.  单击左侧导航栏的**机器列表**。在机器列表页面，可以看到刚刚接入的机器，代表接入成功。

        ![](https://aliware-images.oss-cn-hangzhou.aliyuncs.com/ahas/pg_machine_list.png)

    4.  单击左侧导航栏的**请求链路**，查看已定义的资源。单击右边的“流控”按钮添加新的流控规则：

## 示例二：消息队列 Kafka Consumer 接入示例 {#section_xpl_5ql_zgb .section}

与消息队列 RocketMQ 类似，消息队列 Kafka Consumer 也可通过类似方法接入和使用 AHAS 流控降级服务。

示例：在处理消息的逻辑处定义资源。

``` {#codeblock_h0v_jwa_xm6}
private static void handleMessage(ConsumerRecord<String, String> record, String groupId, String topic) {
    pool.submit(() -> {
        Entry entry = null;
        try {
            // 定义资源。为了便于标识，资源名称定义为 Group ID 和 Topic 的组合。Group ID 和 Topic 可以通过 MQ 控制台获得。
            entry = SphU.entry("handleKafkaMessage:" + groupId + ":" + topic);

            // 业务的消息处理逻辑
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

示例：消费者订阅消息的逻辑

``` {#codeblock_4fx_dsk_kli}
while (true) {
    try {
        ConsumerRecords<String, String> records = consumer.poll(1000);
        // 必须在下次 poll 之前消费完这些数据, 且总耗时不得超过 SESSION_TIMEOUT_MS_CONFIG
        // 建议开一个单独的线程池来消费消息，然后异步返回结果
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

## 相关文档 {#section_fjp_4ns_zgb .section}

本文介绍的是 AHAS 流控降级服务的一个场景 - 请求匀速。AHAS 流控降级服务还可以处理更复杂的各种情况，例如：

-   流量控制：针对不同的调用关系，以不同的运行指标（如 QPS、线程数、系统负载等）为基准，对资源调用进行流量控制，将随机的请求调整成合适的形状（请求匀速、Warm Up 等）。
-   熔断降级：当调用链路中某个资源出现不稳定的情况，如平均响应时间增高、异常比例升高的时候，使对此资源的调用请求快速失败，避免影响其它的资源导致级联失败。
-   系统负载保护：从系统的维度提供保护。当系统负载较高的时候，提供保护机制，让系统的入口流量和系统的负载达到一个平衡，保证系统在能力范围之内处理最多的请求。

您可以参考 [AHAS 流控降级文档](intl.zh-CN/应用流控降级/流控降级概述.md#)探索更多的场景。

