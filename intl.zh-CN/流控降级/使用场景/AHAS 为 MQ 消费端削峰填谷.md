# AHAS 为 MQ 消费端削峰填谷 {#concept_tdp_ly2_zgb .concept}

AHAS 的流控降级模块与 MQ 进行组合，能够从消息的服务端和消费端两个维度保障应用稳定性，让系统负载保持在消息处理水位之下，同时尽可能地处理更多消息，达到“削峰填谷”的效果。

MQ 产品本身具备从服务端保障应用稳定性的能力。本文以 AHAS 的匀速处理请求的能力为例，说明如何对 MQ 消费端进行限流。

## 背景信息 {#section_yjq_cfl_zgb .section}

在消息队列中，当消费者去消费消息的时候，无论是通过 Pull 还是 Push 的方式，都可能会出现大量的消息突刺，如下图中红色部分，消息已超出应用处理能力。如果此时要处理所有消息，很可能会导致系统负载过高，影响稳定性。

消息突刺往往都是瞬时的、不规律的，其后一段时间通常没有消息投递，系统出现空闲资源。若直接把超出处理能力的消息丢掉，则没有充分利用系统处理消息的能力。

最佳的做法是，把消息突刺（图中红色部分）均摊到后面系统空闲时去处理，让系统负载处在一个稳定的水位，同时尽可能地处理更多消息，从而起到“削峰填谷”的效果。此时，我们就需要一个能够控制 MQ 消费端消息匀速处理的利器 - [AHAS 流控降级](https://www.aliyun.com/product/ahas)，来为消息队列削峰填谷，保驾护航。

图示如下：

![](https://aliware-images.oss-cn-hangzhou.aliyuncs.com/ahas/dg_peak_filling.png) 

## 产品组合 {#section_dyw_lgl_zgb .section}

-   [消息队列 （MQ）](https://www.aliyun.com/product/ons)

    消息队列（Message Queue，简称 MQ）是构建分布式互联网应用的基础设施，通过 MQ 实现的松耦合架构设计可以提高系统可用性以及可扩展性，是适用于现代应用的最佳设计方案。

-   [应用高可用服务 AHAS（Application High Availability Service）](https://www.aliyun.com/product/ahas)

    AHAS 流控降级模块，由阿里巴巴内部的限流产品 Sentinel 演化升级而来，久经历年大促的考验，是一款面向分布式服务架构的专业流量控制组件。AHAS 流控降级主要以流量为切入点，从流量控制（限流）、熔断降级、系统保护等多个维度帮助您保障服务的稳定性，同时提供强大的聚合监控和历史监控查询功能。目前客户端支持 Java 语言。


## AHAS 流控降级原理 {#section_wgz_4ml_zgb .section}

在消息队列 MQ 消费端处理消息突刺的场景中，Sentinel 专门提供了[匀速排队](https://help.aliyun.com/document_detail/102571.html#h2-url-3)的控制特性。

它可以把突然到来的大量请求以匀速的形式均摊，以固定的间隔时间让请求通过，以稳定的速度逐步处理这些请求，起到“削峰填谷”的效果，避免流量突刺造成系统负载过高。同时堆积的请求将会排队，逐步进行处理；当请求排队预计超过最大超时时长的时候则直接拒绝，而不是拒绝全部请求。

例如，在 RocketMQ 的场景下，配置匀速模式下请求 QPS 为 5，则每 200 ms 处理一条消息，多余的处理任务将排队；同时配置超时时间为 5 秒，预计的排队时长超过 5 秒的处理任务将会被直接拒绝。

图示如下：

![](https://aliware-images.oss-cn-hangzhou.aliyuncs.com/ahas/dg_waiting_example.png) 

## RocketMQ Consumer 接入示例 {#section_rcj_snl_zgb .section}

下面将介绍如何快速在 RocketMQ Consumer （消费端）接入 AHAS 流控降级 Sentinel。

1.  在 [AHAS 产品主页](https://www.aliyun.com/product/ahas)开通 AHAS 服务。具体步骤，可参考[开通 AHAS 服务](../../../../../intl.zh-CN/准备工作/开通 AHAS 服务.md#)。

2.  在 RocketMQ Consumer 中引入 AHAS Sentinel 的依赖 `ahas-sentinel-client`。以 Maven 为例：

    ```
    <dependency>
        <groupId>com.alibaba.csp</groupId>
        <artifactId>ahas-sentinel-client</artifactId>
        <version>1.1.0</version>
    </dependency>
    ```

3.  由于 RocketMQ Consumer 未提供相应拦截机制，而且每次收到都可能是批量的消息，因此用户需要在处理消息时手动定义资源（埋点）。

    示例：在处理消息的逻辑处手动埋点，并自定义资源名。

    ```
    private static Action handleMessage(Message message, String groupId, String topic) {
            Entry entry = null;
            try {
    		    // 定义资源。为了便于标识，资源名称定义为 Group ID 和 Topic 的组合。Group ID 和 Topic 可以通过 MQ 控制台获得。
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

    示例：消费者订阅消息的逻辑

    ```
    Consumer consumer = ONSFactory.createConsumer(properties);
    consumer.subscribe(topic, "*", (message, context) -> {
        return handleMessage(message);
    });
    consumer.start();
    ```

    关于 RocketMQ 如何订阅消息，请参考 [消息队列 RocketMQ 文档](https://help.aliyun.com/document_detail/34411.html?#h2--5)。

4.  在[AHAS 控制台](https://ahas.console.aliyun.com)，获取 AHAS 启动参数。

1.  在管理控制台最上方地域列表中，选择 Region：

-   若在本地接入的 AHAS 控制台，选择**公网**环境。
-   若在阿里云 ECS 环境，选择对应的 Region 环境。
2.  在左侧导航栏选择**流控降级**，单击右上角**应用接入**。

3.  选择**Java SDK 接入**页签，单击**下一步**到 **配置启动参数**页签，找到启动参数。

    示例如下：

    ```
    -Dproject.name=MqConsumerDemo -Dahas.license=<License>
    ```

    其中，`project.name` 表示应用名，会显示在 AHAS 控制台；`ahas.license` 表示您的授权 License，ECS 环境不需要此项。

5.  在 RocketMQ Consumer 中添加启动参数，启动 Consumer，并向 Consumer 发送消息。

    **说明：** 由于 AHAS 流控降级需要进行资源调用才能触发初始化，因此需要向已进行资源定义的 Group 或 Topic 发送一条消息。具体步骤，可参考[消息队列 RocketMQ 文档](https://help.aliyun.com/document_detail/34411.html?#h2--4)。

6.  Consumer 接收到消息后，在[AHAS 控制台](https://ahas.console.aliyun.com)的流控降级页面查看应用。

    1.  在左侧导航栏选择**流控降级**。

    2.  单击已接入应用的卡片，进入详情页面。

    3.  单击左侧导航栏的**机器列表**。在机器列表页面，可以看到刚刚接入的机器，代表接入成功。

        ![](https://aliware-images.oss-cn-hangzhou.aliyuncs.com/ahas/pg_machine_list.png) 

    4.  单击左侧导航栏的**请求链路**，查看已定义的资源。点击右边的“流控”按钮添加新的流控规则：
7.  在请求链路页面，在对应的请求链路的**操作**栏中，单击**流控**，填写流控规则，并单击**新建**完成创建。

    -   **流控方式**：排队等待
    -   **阈值类型**：QPS，设置 QPS 阈值为 10，代表每 100ms 匀速通过一个请求。
    -   **超时时间**（ms）：2000，超出此超时时间的请求将不会排队，立即拒绝。
    ![](https://aliware-images.oss-cn-hangzhou.aliyuncs.com/ahas/pg_sentinel_app_request_list.png) 

8.  通过 RocketMQ Producer 端向 Consumer 批量发送消息，查看流控效果。
    -   在 Consumer 控制台可以看到消息消费的速率是匀速的，大约每 100ms 消费一条消息。同时，不断有排队的处理任务完成，超出等待时长的处理请求直接被拒绝。

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

    -   在[AHAS 控制台](https://ahas.console.aliyun.com)的应用详情页面，单击**监控详情**，查看消息处理的监控曲线：

        ![](https://aliware-images.oss-cn-hangzhou.aliyuncs.com/ahas/pg_sentinel_app_monitor.png) 

        如果没有使用匀速限流模式，该消息处理的监控曲线会类似于：

        ![](https://aliware-images.oss-cn-hangzhou.aliyuncs.com/ahas/pg_sentinel_app_monitor_vs.png) 

        如果不开启匀速模式，只会同时处理 10 条消息，其余的全部被拒绝。即使后面的时间系统资源充足，多余的请求也无法被处理，因而浪费了许多空闲资源。两种模式对比说明匀速模式下消息处理能力得到了更好的利用。


## Kafka Consumer 接入示例 {#section_xpl_5ql_zgb .section}

与 RocketMQ 类似，Kafka Consumer 也可通过类似方法接入 AHAS 流控降级。下面是一个简单的代码示例：

```
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

```
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

本文介绍的是 AHAS 流控降级 Sentinel 的一个场景 - 请求匀速。Sentinel 还可以处理更复杂的各种情况，比如：

-   流量控制：Sentinel 可以针对不同的调用关系，以不同的运行指标（如 QPS、线程数、系统负载等）为基准，对资源调用进行流量控制，将随机的请求调整成合适的形状（请求匀速、Warm Up 等）。
-   熔断降级：当调用链路中某个资源出现不稳定的情况，如平均 RT 增高、异常比例升高的时候，Sentinel 会使对此资源的调用请求快速失败，避免影响其它的资源导致级联失败。
-   系统负载保护：Sentinel 从系统的维度提供保护。当系统负载较高的时候，Sentinel 提供了对应的保护机制，让系统的入口流量和系统的负载达到一个平衡，保证系统在能力范围之内处理最多的请求。

您可以参考 [AHAS 流控降级文档](intl.zh-CN/流控降级/流控（限流）降级概述.md#)来挖掘更多的场景。

