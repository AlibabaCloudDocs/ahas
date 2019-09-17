# 接入容器服务 Kubernetes 版应用 {#concept_2245240 .concept}

对于部署在容器服务 Kubernetes 版中的 Java 应用，可以使用 AHAS 应用流控降级可以对其配置流控、降级和系统规则来保证系统稳定性。本文将介绍如何将容器服务 Kubernetes 版中的应用接入 AHAS 应用流控降级。

## 前提条件 {#section_i2w_byb_m8d .section}

您已在容器服务 Kubernetes 版控制台上创建 Kubernetes 集群，参见[快速创建Kubernetes集群](../../intl.zh-CN/快速入门/基础入门/快速创建Kubernetes集群.md#)。

## 步骤一：安装 AHAS 组件 {#section_0rv_zpr_lxe .section}

在市场中安装 AHAS 组件后才能将 Java 应用接入 AHAS 应用流控降级，具体步骤如下：

1.  登录[容器服务 Kubernetes 版控制台](https://cs.console.aliyun.com/?spm=5176.2020520152.0.0.2e4316ddwO3DRZ#/k8s/overview)
2.  在控制台左侧导航栏中选择**市场** \> **应用目录**。
3.  在应用目录页面单击**ack-ahas-sentinel-pilot**，然后在**ack-ahas-sentinel-pilot**页面右侧**创建**面板中选择**集群**和**命名空间**，并单击**创建**。

## 步骤二：为 Java 应用开启 AHAS 应用流控降级 {#section_que_2a5_kxx .section}

您可以按需为新建的应用或已有的应用开启 AHAS 应用流控降级。

若需在创建新应用的同时开启 AHAS 应用流控降级，具体步骤如下：

1.  容器服务 Kubernetes 版控制台左侧导航栏中选择**应用** \> **无状态**。
2.  在无状态（Deployment）页面右上角单击**使用模板创建**。
3.  在使用模板创建页面上选择**集群**、**命名空间**和**示例模板**，并在**模板（YAML 格式）**中将以下 `annotations` 添加到 s**pec \> template \> metadata** 层级下：

    完整 YAML 示例模板如下：

    ``` {#codeblock_3hp_oon_wgw}
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


如需为现有应用开启 AHAS 应用流控，操作步骤如下：

1.  容器服务 Kubernetes 版控制台左侧导航栏中选择**应用** \> **无状态**或**应用** \> **有状态**。
2.  在无状态（Deployment）或有状态（StatefulSet）页面上，选择**集群**和**命名空间**，并在目标应用右侧**操作**列中选择**更多** \> **查看 Yaml**。
3.  在编辑 Yaml 对话框中将以下 `annotations` 添加到 **spec \> template \> metadata** 层级下，并单击**更新**。

## 结果验证 {#section_1js_ky1_ie4 .section}

在无状态（Deployment）或有状态（StatefulSet）页面上，目标应用的**操作**列将出现 **AHAS 控制台**按钮。单击 **AHAS 控制台** 即可跳转至 AHAS 控制台。

![result_k8s](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/1781636/156871177860846_zh-CN.png)

## 后续操作 {#section_f5x_yxf_5pr .section}

为应用配置流控降级规则请参见以下文档：

-   [流控规则](intl.zh-CN/应用流控降级/控制台指南/流控规则.md#)
-   [降级规则](intl.zh-CN/应用流控降级/控制台指南/降级规则.md#)
-   [系统规则](intl.zh-CN/应用流控降级/控制台指南/系统规则.md#)

