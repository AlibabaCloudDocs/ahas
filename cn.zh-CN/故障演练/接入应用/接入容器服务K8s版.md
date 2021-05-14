# 接入容器服务K8s版

AHAS架构感知提供了针对容器服务K8s环境的可视化展示能力，自动侦测容器环境包含的ECS主机、容器组、容器、进程和云服务等组件，绘制组件之间的拓扑关系，持续记录，跟踪变化。AHAS的故障演练提供了对容器演练的功能。本文介绍如何将探针接入容器服务K8s版以及如何卸载该探针。

## 前提条件

[快速创建Kubernetes托管版集群](/cn.zh-CN/快速入门/基础入门/快速创建Kubernetes托管版集群.md)

## 接入步骤

在[容器服务管理控制台](https://cs.console.aliyun.com)安装AHAS组件后，即可自动侦测容器环境包含的ECS主机、容器组、容器、进程和云服务等组件。具体步骤如下：

1.  登录[AHAS控制台](https://ahas.console.aliyun.com)，在顶部导航栏选择集群所在地域。
2.  在左侧导航栏选择**探针管理**。
3.  在探针管理页面上方的下拉列表中，选择**添加环境**，并在添加环境对话框中填写环境名称。

    **说明：** 每个地域会有一个默认（Default）环境。您也可以添加自定义环境，如开发环境、测试环境等。不同环境的资源逻辑隔离。

    ![添加环境2.png](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/8973790261/p273733.png)

4.  在探针管理页面，选择**探针安装** \> **安装故障演练探针**。
5.  在安装探针页面，单击**容器服务**。
6.  在应用目录-ack-ahas-pilot页面，单击**参数**页签，可查看安装该组件的默认参数值。

    如需修改，请参考以下参数说明。

    |参数|说明|默认值|
    |--|--|---|
    |`controller.region_id`|目标集群所在的地域，例如cn-hangzhou、cn-beijing、cn-shenzhen。|cn-hangzhou|
    |`resources.requests.cpu`|AHAS Pilot占用的CPU。|0.05|
    |`resources.requests.memory`|AHAS Pilot占用的内存。|200 Mi|
    |`resources.limits.cpu`|AHAS Pilot占用的CPU最高限制，例如，0.2。|0.2|
    |`resources.limits.memory`|AHAS Pilot占用的内存最高限制，例如，200 Mi。|200 Mi|

7.  在应用目录-ack-ahas-pilot页面右侧的**创建**面板中，选择集群，单击**创建**。

## 结果验证

创建完成后，您可以登录[AHAS控制台](https://ahas.console.aliyun.com)，在左侧导航栏选择**探针管理**，在探针管理页面单击**Kubernetes**页签，可查看到接入的集群名称以及探针信息。

## 常见问题

如果探针安装没有成功，请按照以下方式排查：

-   检查是否选择了正确的地域（Region）：

    在AHAS控制台顶部菜单栏选择的地域，需要与安装AHAS Pilot时参数`controller.region_id`配置的地域一致。

    查看参数`controller.region_id`的步骤如下：

    1.  登录[容器服务管理控制台](https://cs.console.aliyun.com)，在左侧导航栏单击**集群**。
    2.  在集群列表页面中，单击目标集群名称或者目标集群右侧**操作**列下的**详情**。
    3.  在集群管理页左侧导航栏中，选择**应用** \> **Helm**。
    4.  找到发布名称为**ahas**的集群，单击**操作**列的**详情**。
    5.  单击**参数**页签，查看地域参数`env.region`的值。
-   检查是否开通了AHAS：

    登录[开通AHAS服务](http://common-buy.aliyun.com/?commodityCode=ahas_001#/buy)页面验证。如果已开通，会提示跳转到AHAS控制台。

-   检查是否已授权AHAS服务：

    登录[授权AHAS服务](https://ram.console.aliyun.com/#/role/authorize?request=%7B%22Requests%22%3A%20%7B%22request1%22%3A%20%7B%22RoleName%22%3A%20%22AliyunAHASDefaultRole%22%2C%20%22TemplateId%22%3A%20%22Default%22%7D%7D%2C%20%22ReturnUrl%22%3A%20%22https%3A//ahas.console.aliyun.com/%23/Setting%3fiis%3d1%26regionId%3dcn-hangzhou%22%2C%20%22Service%22%3A%20%22AHAS%22%7D)页面验证。如未授权，单击**同意授权**。


## 卸载步骤

卸载容器服务中的探针（即AHAS应用高可用服务组件）的步骤如下：

1.  登录[容器服务管理控制台](https://cs.console.aliyun.com)，在左侧导航栏单击**集群**。
2.  在集群列表页面中，单击目标集群名称或者目标集群右侧**操作**列下的**详情**。
3.  在集群管理页左侧导航栏中，选择**应用** \> **Helm**。
4.  找到发布名称为**ahas**的集群，单击其**操作**列的**删除**。
5.  在删除应用的对话框中，选中**清除发布记录**，单击**确定**。

