---
keyword: [ACK, 容器服务, Kubernetes AHAS]
---

# 接入容器服务Kubernetes版应用

对于部署在容器服务Kubernetes版中的Java应用，可以使用AHAS应用防护对其配置流控、降级和系统规则来保证系统稳定性。本文将介绍如何将容器服务Kubernetes版中的应用接入AHAS应用防护。

## 前提条件

[快速创建Kubernetes托管版集群](/cn.zh-CN/快速入门/基础入门/快速创建Kubernetes托管版集群.md)

## 步骤一：安装AHAS组件

在容器服务Kubernetes中安装AHAS组件后才能将Java应用接入AHAS应用防护。

1.  登录[容器服务管理控制台](https://cs.console.aliyun.com)。
2.  在控制台左侧导航栏中选择**市场** \> **应用目录**。
3.  在应用目录页面单击**阿里云应用**页签，选中**ack-ahas-sentinel-pilot**应用。

    **阿里云应用**包含较多应用，您可在页面右上角搜索**ack-ahas-sentinel-pilot**，支持关键字搜索。

4.  在**应用目录 - ack-ahas-sentinel-pilot**页面右侧**创建**区域，选择目标集群，然后单击**创建**。

    ![cluster_ahas_sentinel_pilot_02](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/2306659951/p86637.png)

    |参数|描述|备注|
    |--|--|--|
    |region\_id|    -   如果集群和VPC之间有专线，该参数为专线连接的region。
    -   如果集群和VPC之间没有专线，该参数填入**cn-public**
|根据所选集群自动生成。|
    |cluster\_id|您的集群ID。|
    |cluster\_name|您的集群名称。|


## 步骤二：为Java应用开启AHAS应用防护

您可以按需为新建的应用或已有的应用开启AHAS应用防护。

-   如需在创建新应用的同时开启AHAS应用防护，具体步骤如下：
    1.  登录[容器服务管理控制台](https://cs.console.aliyun.com)。
    2.  在控制台左侧导航栏中，单击**集群**。
    3.  在集群列表页面中，单击目标集群名称或者目标集群右侧**操作**列下的**详情**。
    4.  在集群管理页左侧导航栏中，选择**工作负载** \> **无状态**。
    5.  在无状态（Deployment）页面右上角单击**使用模板创建**。
    6.  在创建页面上选择**示例模板**，并在**模板**中将以下`annotations`添加到**spec \> template \> metadata**层级下，然后单击**创建**。

        如需修改YAML文件中其它配置项，配置项说明如下：

        |Parameter|Description|Default|
        |---------|-----------|-------|
        |image.imageTag|pilot镜像tag。|0.1.1|
        |image.imagePullPolicy|镜像拉取策略，必须是Always、IfNotPresent、Never三者中的一个。|Always|
        |controller.logLevel|pilot日志级别，1表示INFO，2表示DEBBUG。|1|
        |controller.region\_id|目标集群所在的region，如cn-hangzhou、cn-beijing、cn-shenzhen、cn-shanghai。如果是公网，则为cn-public。|cn-hangzhou|

        完整YAML示例模板如下：

        ```
        apiVersion: apps/v1
        kind: Deployment
        metadata:
          name: agent-foo
          labels:
            name: agent-foo
        spec:
          replicas: 1
          selector:
            matchLabels:
              name: agent-foo
          template:
            metadata:
              labels:
                name: agent-foo
              annotations:
                ahasPilotAutoEnable: "on"
                ahasAppName: "K8sFooTest"
                ahasNamespace: "default"
            spec:
              containers:
              - name: foo
                image: registry.cn-hangzhou.aliyuncs.com/sentinel-docker-repo/foo:0.1.1
                imagePullPolicy: Always          
        ```

-   如需为现有应用开启AHAS应用防护，操作步骤如下。
    1.  登录[容器服务管理控制台](https://cs.console.aliyun.com)。
    2.  在控制台左侧导航栏中，单击**集群**。
    3.  在集群列表页面中，单击目标集群名称或者目标集群右侧**操作**列下的**详情**。
    4.  在集群管理页左侧导航栏中，选择**工作负载** \> **无状态**或**工作负载** \> **有状态**。
    5.  在无状态（Deployment）或有状态（StatefulSet）页面上，单击目标应用右侧**操作**列中选择**更多** \> **查看YAML**。
    6.  在编辑YAML对话框中将以下`annotations`添加到**spec \> template \> metadata**层级下，并单击**更新**。

## 结果验证

1.  登录[容器服务管理控制台](https://cs.console.aliyun.com)。
2.  在控制台左侧导航栏中，单击**集群**。
3.  在集群列表页面中，单击目标集群名称或者目标集群右侧**操作**列下的**详情**。
4.  在集群管理页左侧导航栏中，选择**工作负载** \> **无状态**或**工作负载** \> **有状态**。

在目标应用的**操作**列将出现**应用流控**按钮。单击**应用流控**即可跳转至[AHAS控制台](https://ahas.console.aliyun.com)。

![result_k8s](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/0633858951/p60846.png)

