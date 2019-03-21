# 通过容器服务 Kubernetes 快速接入 {#concept_yrs_vj1_chb .concept}

AHAS 架构感知提供了针对容器服务 Kubernetes 环境的可视化展示能力，自动侦测容器环境包含的 ECS 主机、容器组、容器、进程和云服务等组件，绘制组件之间的拓扑关系，持续记录，跟踪变化。

AHAS 架构感知能够展现每个容器组的详细信息以及与容器、进程、主机等组件之间的依赖关系。

## 前提条件 {#section_m3l_3l1_chb .section}

-   [创建Kubernetes集群](../../../../../intl.zh-CN/用户指南/Kubernetes集群/集群管理/创建Kubernetes集群.md#)
-   [开通 AHAS 服务](../../../../../intl.zh-CN/准备工作/开通 AHAS 服务.md#)

## 操作步骤 {#section_c5r_sl1_chb .section}

安装 AHAS 应用高可用服务组件的步骤如下：

1.  访问[云资源访问授权](https://ram.console.aliyun.com/#/role/authorize?request=%7B%22Requests%22%3A%20%7B%22request1%22%3A%20%7B%22RoleName%22%3A%20%22AliyunAHASDefaultRole%22%2C%20%22TemplateId%22%3A%20%22Default%22%7D%7D%2C%20%22ReturnUrl%22%3A%20%22https%3A//ahas.console.aliyun.com/%23/Setting%3fiis%3d1%26regionId%3dcn-hangzhou%22%2C%20%22Service%22%3A%20%22AHAS%22%7D)页面，单击**同意授权**。
2.  登录[容器服务 - Kubernetes管理控制台](https://cs.console.aliyun.com/?spm=a2c4g.11186623.2.17.66d75bc79AYTH7)。
3.  在左侧导航栏中，选择**市场** \> **应用目录**，单击 **ack-ahas-pilot**。
4.  在应用目录-ack-ahas-pilot页面，单击**参数**页签，可查看安装该组件的默认参数。如需修改，详见[参数说明](#section_gmb_m41_chb)。
5.  在应用目录-ack-ahas-pilot页面右侧的**创建**区域，选择集群、命名空间，并自定义发布名称，单击**创建**，添加 AHAS 应用高可用服务组件。

创建完成后，您可以登录 [AHAS 控制台](https://ahas.console.aliyun.com)，查看 AHAS 服务数据。详见[架构感知概述](intl.zh-CN/架构感知/架构感知概述.md#)。

## 参数说明 {#section_gmb_m41_chb .section}

下表介绍了 ack-ahas-pilot 组件的相关参数。

|参数|说明|默认值|
|--|--|---|
|`env.region` |目标集群所在的地域，例如 cn-hangzhou、cn-beijing、 cn-shenzhen。|cn-hangzhou|
|`resources.requests.cpu`|AHAS pilot 占用的 CPU|0.05|
|`resources.requests.memory`|AHAS pilot 占用的 Memory|128 M|
|`resources.limits.cpu`|AHAS pilot 占用 CPU 限制为 0.2 核|0.2|
|`resources.limits.memory`|AHAS pilot 占用的 Memory 限制为 128M|128 M|

