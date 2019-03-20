# PTS 和 AHAS 共同保障应用稳定性 {#concept_ssl_jy2_zgb .concept}

本文通过介绍性能测试 PTS 与 AHAS 流控降级产品组合的典型应用场景，帮助您了解 PTS 与 AHAS 流控降级是如何保障应用稳定性的。

## 背景信息 {#section_urm_k3f_zgb .section}

服务端的性能测试，特别是业务性能测试，目的主要是评估性能容量、诊断性能瓶颈、诊断应用错误，甚至是验证高可用的能力，从而通过针对性的优化达到降低成本、提升用户体验的目的。

而在评估出系统容量后，您通常需要根据系统可承载的极限，设置对应的限流阈值，以防突发的流量洪峰超出系统可承载的最大值而引发雪崩效应。AHAS 流控降级模块能够从流量控制（限流）、熔断降级、系统保护等多个维度帮助您保障服务的稳定性。

## 产品组合 {#section_i1p_wbf_zgb .section}

-   [性能测试 PTS（Performance Testing Service）](https://www.aliyun.com/product/pts)

    PTS 是面向所有技术相关背景人员的云化性能测试工具，孵化自阿里巴巴内部平台。有别于繁复的传统工具，PTS 以互联网化的交互，面向分布式和云化的设计，更适合当前的主流技术架构。无论是自研还是适配开源的功能，PTS 都可以轻松模拟大量用户访问业务的场景，随时发起任务，免去搭建和维护成本。同时，紧密结合监控类产品提供一站式监控、定位等附加价值，高效检验和管理业务性能。

-   [应用高可用服务 AHAS（Application High Availability Service）](https://www.aliyun.com/product/ahas)

    AHAS 流控降级模块，由阿里巴巴内部的限流产品 Sentinel 演化升级而来，支持了天猫双 11、双 12 及年货年等大促活动，是一款面向分布式服务架构的专业流量控制组件。AHAS 流控降级主要以流量为切入点，从流量控制（限流）、熔断降级、系统保护等多个维度保障服务的稳定性，同时提供强大的聚合监控和历史监控查询功能。目前客户端支持 Java 语言。

    和常见的网关限流相比，AHAS 流控降级有以下优势：

    -   精细的防护粒度

        支持自定义接口资源，可以根据 QPS（Queries Per Second）、线程、系统负载等多种指标进行限流或者降级。

    -   全方位的监控

        支持查看接口的实时、历史监控数据，以更加友好的界面展现当前资源通过的 QPS、拒绝的 QPS、响应时间等信息，同时支持查看单机指定资源的监控数据。

    -   多种主流框架适配

        提供 Web Servlet、Dubbo、Spring Boot、Spring Cloud、gRPC、Apache RocketMQ、Netflix Zuul 等多种框架的适配，只需要引入相应的依赖并进行少量配置即可接入。

    -   良好的性能

        客户端的性能损耗非常小。只有在单机业务量级超过 25 万 QPS 的时候才会有一些显著的影响（10% 左右），单机 QPS 不大时损耗几乎可以忽略不计，详见[性能测试报告](https://github.com/alibaba/Sentinel/wiki/Benchmark)。


## 适用行业 {#section_twl_1cf_zgb .section}

PTS 与 AHAS 共同组成的压测流控方案，不仅在阿里巴巴内部淘宝、天猫等电商领域有着广泛的应用，在互联网金融、游戏行业、直播行业和其他大型政央企行业也有着大量的实践。通过 PTS 进行系统验证，提早发现性能短板的同时，通过 AHAS 进行流量防控，进一步确保系统的稳定性。

## 最佳实践 {#section_ewz_ccf_zgb .section}

下面简要介绍如何通过 PTS 和 AHAS 进行流量防控。

1.  根据您的业务场景，通过 PTS 构建高仿真业务压测，验证系统能够支持的最大并发请求量。
2.  压测停止后，在压测报告中可查看当前系统的最大并发请求量。

    ![](https://aliware-images.oss-cn-hangzhou.aliyuncs.com/ahas/sc_pts_report.png)

3.  假设某重要接口经过多次优化和压测后达到了业务预期的 QPS，系统机器资源也是按照该访问量配置的。如果用户请求超过该预期值，可能会导致 CPU、负载飚高，随之引发一系列问题影响正常用户访问。

    那么，我们就需要通过 AHAS 流控降级功能对该接口资源设置相应的流控规则，将限流阈值设置为期望限制的 QPS 值。

    ![](https://aliware-images.oss-cn-hangzhou.aliyuncs.com/ahas/sc_example_pts_and_ahas.png)

4.  默认情况下，新建的流控或降级规则立即生效。在 AHAS 流控降级监控页面，您可以实时查看该接口资源的通过的 QPS 和拒绝的 QPS。

    ![](https://aliware-images.oss-cn-hangzhou.aliyuncs.com/ahas/sc_example2_pts_and_ahas.png)

    这样就能保证系统一直处于期望的安全水位之内，即使出现突发的流量，也不用担心资源耗尽系统被拖垮。


## 相关文档 {#section_mrl_jcf_zgb .section}

-   关于 AHAS 流控降级的接入和使用，请参考[开通 AHAS 服务](../../../../../cn.zh-CN/准备工作/开通 AHAS 服务.md#)、[接入](cn.zh-CN/流控降级/接入/通过 SDK 接入/Dubbo 应用接入.md#)和[规则配置](cn.zh-CN/流控降级/控制台指南/流控规则.md#)。
-   关于 PTS 的开通和使用，请参考[开通服务](https://help.aliyun.com/document_detail/55787.html)、[创建压测场景](https://help.aliyun.com/document_detail/90887.html)和[启动压测](https://help.aliyun.com/document_detail/72469.html)。

