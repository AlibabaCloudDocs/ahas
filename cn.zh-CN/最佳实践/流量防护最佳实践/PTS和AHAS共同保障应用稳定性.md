---
keyword: [PTS, 系统防护, 流控, 降级, 隔离, 稳定性]
---

# PTS和AHAS共同保障应用稳定性

为提高应用高可用性，可以结合使用PTS与AHAS。首先使用PTS压测评估系统瓶颈，然后使用AHAS以系统瓶颈指标为阈值设置流控、降级、系统或隔离规则，保障系统稳定性。

## 背景信息

随着应用系统的频繁迭代，保障应用系统的稳定性越来越重要。主要原因如下：

-   随着应用上云的普及，单机架构向分布式架构演进，系统之间的依赖关系、调用链路变的十分复杂。
-   业务发展带来的服务端迭代越来越快，在性能管理上很难有足够的投入，经常会产生未知的隐患导致性能的大幅下降。

行业痛点：

-   对系统提供服务的能力不清楚，不知道如何进行压测，写脚本门槛太高。
-   压测工具维护很麻烦，压测流量不稳定，施压能力有限。
-   业务接口没有流量保护，瞬间流量超过上限就会压垮系统。
-   下游依赖服务不稳定，经常调用超时影响核心接口，影响系统稳定性。
-   非关键业务调用占用太多资源，核心业务的稳定性。

## 解决方案

借助于阿里巴巴内部多年高可用体系沉淀下来的经验，结合使用[性能测试PTS](https://www.aliyun.com/product/pts)和[应用高可用服务AHAS](https://www.aliyun.com/product/ahas)，即可从压测、流量防护两个维度协助保障应用的稳定性。PTS是具备强大分布式压测能力的SaaS压测平台，可模拟海量用户的真实业务场景，全方位验证业务站点的性能、容量和稳定性。AHAS则以流量为切入点，从流量控制、熔断降级、热点防护和系统保护等多个维度来帮助保障服务的稳定性，同时提供秒级的流量监控分析功能。

## 产品优势

## 经典案例

PTS和AHAS组成的压测流控方案，不仅在阿里内部淘宝、天猫等电商领域有着广泛的应用，在互联网金融、在线教育、游戏、直播行业和其他大型政央企行业也有着大量的实践。

在新冠疫情防护中，PTS和AHAS一体化的压测和防护为全国各地区的健康码提供了强有力的支撑。通过PTS平台对支付宝健康码服务进行压测，测出系统对外核心接口的服务能力以及相应的系统水位。同时使用AHAS根据压测结果中不同接口和系统指标配置限流、隔离以及系统保护等规则，在最短的时间内接入应用并持续提供防护，保障系统稳定性。

## 使用方法

1.  开通服务并购买资源包。
    -   [开通 PTS 服务]()。
    -   [开通 AHAS](/cn.zh-CN/快速入门/开通 AHAS.md)。
2.  容量评估。
    1.  使用PTS快速构建高仿真业务压测并发起压测，详情请参见[如何在一分钟内发起压测？]()。

        压测过程中可以在**场景详情**页签中查看各API的压测信息。例如本示例中**选课提交** API出现非2xx错误5/s。

        ![容量评估1](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/5718029951/p87282.png)

    2.  在PTS控制台观察压测发起侧（客户侧）及服务侧（云监控）的端到端全监控，详情请参见[查看监控详情]()，了解压测下的业务表现和各核心系统的性能水位情况。
3.  设置流控、降级、系统和隔离规则。
    1.  将应用接入AHAS，详情请参见[接入应用概述](/cn.zh-CN/流量防护/应用防护/接入应用/接入应用概述.md)。
    2.  根据所压测接口的RT响应情况、系统负载以及当前压测的请求量为接口配置流控、降级、系统和隔离规则。
        -   [配置流控规则](/cn.zh-CN/流量防护/应用防护/配置规则/配置流控规则.md)：流控规则一般用于入口流量的防护，避免突发流量超过系统所能承受的最大值而压垮系统。
        -   [配置降级规则](/cn.zh-CN/流量防护/应用防护/配置规则/配置降级规则.md)：对于系统中存在的弱依赖服务，为了避免依赖的下游服务不可用拖累整个系统，可以在调用方设置降级规则。
        -   [自适应流控](/cn.zh-CN/流量防护/应用防护/配置规则/自适应流控.md)：为系统设置整体防护规则，对于CPU、Load等指标超过设定的阈值时触发系统限流，保障系统整体的可用性。
        -   [配置隔离规则](/cn.zh-CN/流量防护/应用防护/配置规则/配置隔离规则.md)：对于线程资源消耗比较多的接口，可以创建隔离规则，避免该接口在并发量大的情况下占用过多系统资源导致线程池满等问题。
4.  配置流量大盘，详情请参见[创建流量大盘](/cn.zh-CN/流量防护/创建流量大盘.md)。

    通过监控详情提供的多方位监控指标，动态调整接口的规则阈值并实时推送。

    ![流量大盘](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/5718029951/p87303.png)


## 相关文档

-   关于AHAS应用防护的接入和使用，请参见[开通 AHAS](/cn.zh-CN/快速入门/开通 AHAS.md)、[接入](/cn.zh-CN/流量防护/应用防护/接入应用/接入JAVA SDK应用/接入Dubbo应用.md)和[规则配置](/cn.zh-CN/流量防护/应用防护/配置规则/配置流控规则.md)。
-   关于PTS的开通和使用，请参见[开通服务](https://help.aliyun.com/document_detail/55787.html)、[创建压测场景](https://help.aliyun.com/document_detail/90887.html)和[启动压测](https://help.aliyun.com/document_detail/72469.html)。



