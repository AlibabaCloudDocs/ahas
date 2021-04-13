---
keyword: [Mesh, Istio, Envoy]
---

# Mesh防护

AHAS为网格化应用提供控制全局流量的能力，例如Istio、Envoy服务网格。本文介绍如何在AHAS中接入Istio服务网格（包括阿里云服务网格ASM）、Envoy集群并为其配置流控规则。

已开通AHAS专业版，若没有开通，请进入[开通页面](https://common-buy.aliyun.com/?commodityCode=ahas_post#/open)。

阿里云服务网格ASM（Alibaba Cloud Service Mesh）提供了一个全托管式的服务网格平台，兼容于社区Istio开源服务网格，用于简化服务的治理。更多信息，请参见[什么是服务网格ASM？]()。AHAS Mesh防护基于Envoy Global Rate Limiting Service（RLS）接口实现，防护原理如下图所示。

![Mesh防护原理图.png](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/1070008951/p142317.png)

**说明：** Service Mesh与AHAS Token Server的通信会带来一定的网络开销，响应时间可能会略有上升（同个Region一般会在2 ms~5 ms左右）。

## 操作步骤

1.  登录[AHAS控制台](https://ahas.console.aliyun.com)，在左侧导航栏选择**流量防护** \> **Mesh防护**。

2.  单击页面右上角的**申请Mesh流控集群**。

3.  在防护详情页面，填写**集群名称**等信息。

    |参数|描述|
    |--|--|
    |**集群名称**|填写集群的名称。集群名称应包含1~63个字符。|
    |**Envoy流控domain**|流控服务的域，需要与[步骤5](#step_a7b_95u_p89)中要配置的EnvoyFilter里面的domain相对应。|
    |**集群预计QPS**|该集群内需要流控的接口预估的最大QPS，代表可能到来的最大流量，而非限流阈值，用于为Token Server自动分配提供参考。|

4.  单击**下一步**，集群申请成功。

5.  单击**Mesh流控接入**，可选择接入Istio或Envoy。

    -   **接入Istio**

        AHAS为Istio服务网格提供集群流控的能力。要为Istio集群接入AHAS Mesh流控，需要为Istio创建对应的EnvoyFilter CRD配置。

        1.  单击**Istio接入**页签。
        2.  复制代码，将其粘贴至新建的YAML文件中。
        3.  在Istio集群中，通过执行`kubectl apply`命令使其生效，完成接入。
        **说明：** 目前Istio流控基于Envoy global rate limiting实现，支持根据来源集群、目标集群、Header值等请求属性进行流控，详情请参见[Envoy相关文档](https://www.envoyproxy.io/docs/envoy/latest/configuration/http/http_filters/rate_limit_filter?spm=5176.11961263.SystemGuardMeshProtection.4.f92f3bc10j41b0#config-http-filters-rate-limit)。

    -   **接入Envoy**

        AHAS为Envoy HTTP流量提供集群流控的能力。Envoy接入需要按下面步骤编辑Envoy配置文件。

        1.  单击**Envoy接入**页签。
        2.  复制页面中第一步的示例代码，为需要进行流控的路由（route）所在的VirtualHost配置流控项（rate\_limits），流控项由一系列的流控参数rate\_limit\_action构成。

            **说明：**

            -   action里面的generic\_key需要配置成AHAS集群流控的license，否则流控将不会生效。该项将不会作为流控的判断属性。当前集群流控的license会在页面的代码中显示。
            -   Envoy目前支持根据来源集群、目标集群、通用标识（generic\_key）、Header值等请求属性进行流控，详情请参考[Envoy相关文档](https://www.envoyproxy.io/docs/envoy/latest/configuration/http/http_filters/rate_limit_filter?spm=5176.11961263.SystemGuardMeshProtection.6.f92f3bc10j41b0#config-http-filters-rate-limit)。
        3.  复制页面中第二步的示例代码，在Clusters中添加AHAS Mesh流控Cluster，配置对应的RLS token server IP和端口。
        4.  复制页面中第三步的示例代码，在http\_filters中添加envoy.rate\_limit配置，指定上一步配置的AHAS Mesh流控Cluster。
        5.  配置文件修改完成后，重启Envoy或通过xDS动态reload配置文件，完成接入。
6.  在集群规则配置区域，单击**添加**，进入规则配置对话框，为目标集群添加规则。

    |参数|描述|
    |--|--|
    |**规则名称**|用于标识该规则，不超过64个字符，规则名称不能重复。|
    |**阈值**|集群阈值，满足流控条件的请求量到达该阈值后会被拒绝。|
    |**统计窗口时长**|集群流控统计的时间窗口长度，取值范围为1秒~24小时。|
    |**匹配规则**|流控针对的请求属性的匹配规则，如针对不同来源的请求分别限制不同的规则。目前支持以下匹配规则（与Envoy descriptor保持一致）：    -   来源集群：source\_cluster。
    -   目标集群：destination\_cluster。
    -   通用标识：generic\_key。
    -   自定义：自定义Key，名称不可重复。 |

7.  单击**确定**，完成规则创建。

    **执行结果：**

    触发Mesh中的服务调用，观察服务的返回值来判断流控是否生效。返回`429 Too Many Requests`状态码即表示流控成功。


