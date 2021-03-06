---
keyword: [sentinel, 应用防护, 商业化, 开源]
---

# 开源Sentinel与商业化AHAS流量防护对比

Sentinel是面向分布式服务架构的轻量级流量控制产品，主要以流量为切入点，从流量控制、熔断降级、系统负载保护等多个维度来保护服务的稳定性。AHAS流量防护是开源框架Sentinel的商业化产品，是阿里巴巴双十一技术体系中的核心组件，它在Sentinel的基础上，支持更多的业务功能。本文介绍AHAS流量防护与开源Sentinel的对比优势。

## 应用侧

**核心能力**

|功能描述|AHAS流量防护|开源Sentinel|
|----|--------|----------|
|基础的流控降级、系统保护功能|支持|支持|
|慢SQL识别与熔断|支持|不支持|
|缓存防护 \(Redis、Memcached\)|支持|不支持|
|全自动托管、高可用的集群流控服务|支持|不支持|
|托管的Service Mesh集群流控|支持|不支持|
|渐进式熔断降级策略|支持|不支持|
|K8s自动弹性|支持|不支持|
|PHP应用高可用防护|支持|不支持|

**快速接入**

|功能描述|AHAS流量防护|开源Sentinel|
|----|--------|----------|
|Java Agent方式无侵入快速接入|支持近20种主流框架|不支持|
|K8s应用快速接入|支持近20种主流框架|不支持|
|PHP、Go应用快速接入|支持|不支持|

## 运维侧

|功能描述|AHAS流量防护|开源Sentinel|
|----|--------|----------|
|控制台实时秒级监控|支持接口和应用维度监控，支持按调用类型分类，支持QPS、RT、CPU usage、Load等指标。|有限的支持（内存存储5分钟）|
|Top N接口统计|支持|不支持|
|流量同比、环比展示|支持|不支持|
|历史监控查询|支持|不支持|
|机器热力图|支持|不支持|
|业务场景流量大盘|支持|不支持|
|规则实时推送|秒级生效，实时可靠。|HTTP方式推送，不可靠。|
|规则管理|多重持久化，高可用。|内存存储，不可靠。|
|流控自动触发报警|支持|不支持|
|主子账号权限控制|支持|不支持|

## AHAS流量防护优势

**应用侧**

除了支持开源Sentinel的功能，AHAS流量防护还额外支持许多其他功能，具体如下：

-   慢SQL识别与熔断场景（MyBatis、MySQL JDBC、Oracle JDBC）。
-   缓存防护场景（Redis、Memcached）。
-   针对通用场景的渐进式熔断降级策略。
-   全自动托管、高可用的集群流控服务，后续还会支持分钟小时级别流控、集群并发控制等能力。
-   托管的Service Mesh集群流控服务，支持Envoy、Istio集群快速接入。
-   容器弹性，支持根据应用实时QPS、RT进行自动扩缩容。
-   PHP应用高可用防护支持。

AHAS流量防护还提供多种快速接入的方式：

-   Java Agent方式或K8s Java应用零侵入快速接入，支持近20种主流框架和API Gateway。
-   K8s Java应用零侵入快速接入，支持近20种主流框架和API Gateway。
-   PHP、Go应用快速接入。

**运维侧**

AHAS流量防护拥有企业级的控制台，而Sentinel开源控制台仅提供基本的功能示例。AHAS流量防护控制台包括以下功能：

-   可靠的实时监控和历史秒级监控数据查询，包含接口维度的QPS、响应时间及系统Load、CPU使用率等指标，支持按照调用类型分类，支持同比、环比展示。
-   Top K接口监控统计，快速了解系统的慢调用和大流量接口。
-   热力图概览，快速定位不稳定的机器。
-   业务场景流量大盘，便于关注多个系统的整体流量情况。
-   海量规则管理和实时推送，秒级生效，实时可靠。
-   告警中心（触发流控、CPU使用率高等事件），支持通过钉钉机器人等形式自动触发报警。
-   细粒度的权限控制支持。
-   控制台快速配置接口限流的处理逻辑。

## 参考文档

[Sentinel介绍](https://github.com/alibaba/Sentinel)

