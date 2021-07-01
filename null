---
keyword: [Nginx, 流控功能, 高可用防护功能]
---

# 使用Ingress-sentinel实现流控

ACK提供了Ingress-sentinel流控功能，通过Ingress-sentinel流控功能可以快速接入到AHAS中。当有请求流量时，您可以在AHAS控制台中查看Nginx网关请求的实时QPS和RT等数据。本文介绍如何使用Ingress-sentinel功能实现流控。

-   [开通AHAS](/cn.zh-CN/快速入门/开通AHAS.md)
-   [创建Kubernetes托管版集群](/cn.zh-CN/Kubernetes集群用户指南/集群/创建集群/创建Kubernetes托管版集群.md)
-   请确保ACK集群中的Ingress Controller运行正常，且不低于0.44.0版本。

应用高可用服务AHAS（Application High Availability Service）提供了应用架构探测感知，故障注入式高可用能力评测和流控降级高可用防护三大核心能力，其中针对Nginx的流控降级高可用防护功能已集成到ACK提供的Ingress-Nginx-Controller中，您可用根据实际需求开启该功能，查看流控数据。

## 使用限制

开启Ingress-sentinel流控功能，会消耗一定的系统资源。您使用的机器需要符合一定的配置，以下为配置说明：

-   最低配置：CPU为1000m Core，内存为2048 MiB。
-   建议配置：CPU为4000m Core及以上，内存为8192 MiB及以上。

## 开启Ingress-sentinel流控功能

1.  登录[容器服务管理控制台](https://cs.console.aliyun.com)。

2.  在控制台左侧导航栏中，单击**集群**。

3.  在集群列表页面中，单击目标集群名称或者目标集群右侧**操作**列下的**详情**。

4.  在集群管理页左侧导航栏中，选择**配置管理** \> **配置项**。

5.  在配置项页面名称搜索框中搜索nginx-configuration，找到nginx-configuration，然后单击nginx-configuration**操作**列的**编辑**。

6.  自定义应用名称。

    在**编辑**面板单击**添加**，设置**名称**为sentinel-params ，**值**为--app=demo-k8s-2020。

    **说明：** --app=demo-k8s-2020字段中demo-k8s-2020为应用名称，您可以根据实际需求替换应用名称。

7.  如果您的集群所在地域不属于深圳、北京、上海、张家口、杭州，则还需要配置证书。

    单击**添加**，设置**名称**为sentinel-params ，**值**为--app=demo-k8s --license=xxx。

    **说明：** 关于获取License的更多信息，请参见[查看License](/cn.zh-CN/应用防护/参考信息/查看License.md)。

8.  如果您希望接收到超过流控配置上限的请求时，系统能够返回HTTP 429错误码（表示请求数过多）。则您可以配置流控HTTP返回码。

    单击**添加**，设置**名称**为sentinel-block-action，**值**为=429。

    **说明：** 如果您想要自定义HTTP错误码，可以根据实际需求修改429。

9.  开启Ingress-sentinel流控功能。

    **说明：** 接入Ingress-sentinel流控功能后默认不会触发流控，只有配置开启流控规则，并且请求流量超过流控规则限制后才会触发流控。

    单击**添加**，设置**名称**为use-sentinel，**值**为true。然后单击**确定**。


## 配置流控规则

登录[AHAS控制台](https://ahas.console.aliyun.com)，在控制台左侧导航栏选择**流量防护** \> **Nginx防护**，单击目标应用卡片，可以看到应用名称对应的流控监控窗口。具体操作请参见[配置流控规则](/cn.zh-CN/应用防护/配置规则/配置流控规则.md)、[配置隔离规则](/cn.zh-CN/应用防护/配置规则/配置隔离规则.md)或[配置熔断规则](/cn.zh-CN/应用防护/配置规则/配置熔断规则.md)。

![流控窗口](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/5792825161/p247227.png)

如果您需要配置更详细的流控规则，请参见[管理API](/cn.zh-CN/Ingress/Nginx防护/管理API.md) 和[配置流控规则](/cn.zh-CN/Ingress/Nginx防护/配置流控规则.md)。规则配置完成后，您可以在应用概览页面实时查看流控指标。

![流控指标](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/3105911161/p227294.png)

