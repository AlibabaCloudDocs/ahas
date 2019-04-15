# 通过容器服务 Kubernetes 快速接入 {#concept_yrs_vj1_chb .concept}

应用高可用服务（Application High Availability Service，简称 AHAS）架构感知提供了针对容器服务 Kubernetes 环境的可视化展示能力，自动侦测容器环境包含的 ECS 主机、容器组、容器、进程和云服务等组件，绘制组件之间的拓扑关系，持续记录，跟踪变化。

## 前提条件 {#section_m3l_3l1_chb .section}

-   您已创建容器服务 Kubernetes 集群。具体步骤，参见[创建Kubernetes集群](../../../../../intl.zh-CN/用户指南/Kubernetes集群/集群管理/创建Kubernetes集群.md#)

-   您已开通 AHAS。具体步骤，参见[开通 AHAS 服务](../../../../../intl.zh-CN/准备工作/开通 AHAS 服务.md#)

## 安装步骤 {#section_c5r_sl1_chb .section}

安装 AHAS 组件的步骤如下：

1.  访问[云资源访问授权](https://ram.console.aliyun.com/#/role/authorize?request=%7B%22Requests%22%3A%20%7B%22request1%22%3A%20%7B%22RoleName%22%3A%20%22AliyunAHASDefaultRole%22%2C%20%22TemplateId%22%3A%20%22Default%22%7D%7D%2C%20%22ReturnUrl%22%3A%20%22https%3A//ahas.console.aliyun.com/%23/Setting%3fiis%3d1%26regionId%3dcn-hangzhou%22%2C%20%22Service%22%3A%20%22AHAS%22%7D)页面，单击**同意授权**。
2.  登录[容器服务 - Kubernetes管理控制台](https://cs.console.aliyun.com)。
3.  在左侧导航栏中，选择**市场** \> **应用目录**，单击 **ack-ahas-pilot**。
4.  在应用目录-ack-ahas-pilot页面，单击**参数**页签，可查看安装该组件的默认参数值。

    如需修改，请参考以下参数说明。

    |参数|说明|默认值|
    |--|--|---|
    |`controller.region_id`|目标集群所在的地域，例如 cn-hangzhou、cn-beijing、cn-shenzhen。|cn-hangzhou|
    |`resources.requests.cpu`|AHAS Pilot 占用的 CPU|0.05|
    |`resources.requests.memory`|AHAS Pilot 占用的内存|200 Mi|
    |`resources.limits.cpu`|AHAS Pilot 占用的 CPU 最高限制为，例如，0.2。|0.2|
    |`resources.limits.memory`|AHAS Pilot 占用的内存最高限制为，例如，200 Mi。|200 Mi|

5.  在应用目录-ack-ahas-pilot页面右侧的**创建**区域，选择集群、命名空间，并自定义发布名称，单击**创建**，添加 AHAS 组件。

创建完成后，您可以登录 [AHAS 控制台](https://ahas.console.aliyun.com)，查看 AHAS 服务数据。

如果**概览**页中架构感知容器组数为 0，或者架构感知中数据为空，请排查以下项：

-   检查是否选择了正确的地域（Region）：在 AHAS 控制台左上角选择的地域，需要与安装 AHAS Pilot 时参数`controller.region_id`配置的地域一致。

    查看参数`controller.region_id`的步骤如下：

    1.  在[容器服务 - Kubernetes管理控制台](https://cs.console.aliyun.com)左侧导航栏，选择**应用** \> **发布**。
    2.  在发布页面，选择 **Helm** 页签。
    3.  找到发布名称为 **ahas** 的集群，单击**操作**列的**详情**。
    4.  单击**参数**页签，查看地域参数`env.region`的值。
-   检查是否开通了 AHAS：访问[开通 AHAS 服务](http://common-buy.aliyun.com/?commodityCode=ahas_001#/buy)页面验证。如果已开通，会提示跳转到 AHAS 控制台。
-   检查是否已授权 AHAS 服务：访问[授权 AHAS 服务](https://ram.console.aliyun.com/#/role/authorize?request=%7B%22Requests%22%3A%20%7B%22request1%22%3A%20%7B%22RoleName%22%3A%20%22AliyunAHASDefaultRole%22%2C%20%22TemplateId%22%3A%20%22Default%22%7D%7D%2C%20%22ReturnUrl%22%3A%20%22https%3A//ahas.console.aliyun.com/%23/Setting%3fiis%3d1%26regionId%3dcn-hangzhou%22%2C%20%22Service%22%3A%20%22AHAS%22%7D)页面验证。如未授权，单击**同意授权**。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/138297/155531027644380_zh-CN.png)


架构感知的详细信息，参见[架构感知概述](intl.zh-CN/架构感知/架构感知概述.md#)。

## 卸载步骤 {#section_gmb_m41_chb .section}

卸载 AHAS 应用高可用服务组件的步骤如下：

1.  登录[容器服务 - Kubernetes管理控制台](https://cs.console.aliyun.com)。
2.  在左侧导航栏中，选择**应用** \> **发布**。
3.  单击 **Helm** 页签。
4.  找到发布名称为 **ahas** 的集群，单击其**操作**列的**删除**。

