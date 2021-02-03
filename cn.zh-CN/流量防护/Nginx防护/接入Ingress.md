---
keyword: [Ingress Nginx, ACK, Nginx防护]
---

# 接入Ingress

Ingress是Kubernetes中的一个资源对象，用来管理集群外部访问集群内部服务的方式。AHAS支持Ingress接入Nginx防护，然后对其设置流控规则，实现应用的高可用。本文介绍如何接入Ingress。

目前AHAS控制台接入Ingress只支持深圳、北京、上海、张家口、杭州五个地域。在其他地域创建的ACK集群，AHAS控制台即使接入Ingress也无法生效。

## 接入Ingress

1.  登录[容器服务管理控制台](https://cs.console.aliyun.com)，创建ACK集群。具体操作，请参见[创建Kubernetes托管版集群](/cn.zh-CN/Kubernetes集群用户指南/集群管理/创建集群/创建Kubernetes托管版集群.md)。

    在创建ACK集群时，必须选中**安装Ingress组件**。

    ![安装Ingress组件.png](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/7483522161/p237763.png)

2.  在[容器服务管理控制台](https://cs.console.aliyun.com)左侧导航栏中，单击**集群**。然后在集群列表页面中，单击目标集群名称或者目标集群右侧**操作**列下的**详情**。

3.  在集群管理页左侧导航栏中，选择**工作负载** \> **无状态**。

4.  在无状态页面顶部选择**命名空间**为**kube-system**，在无状态列表单击**nginx-ingress-control****操作**列的**编辑**。

    ![替换镜像.png](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/7483522161/p237832.png)

5.  在编辑页面，单击**nginx-ingress-control**页签，设置以下参数，然后单击**更新**。

    1.  设置**镜像名称**为**registry.cn-hangzhou.aliyuncs.com/ahas/ahas-ingress-control**。

    2.  设置**镜像Tag**为**v1.0.7-6ebc13dc545c**。

    3.  设置**所需资源**的**CPU**为**1000m** Core，**内存**为**2048** MiB。其他参数保持默认设置。

        **说明：** 由于引入流控功能会带来一些资源消耗，所以建议您设置Ingress最小配置CPU为1000m Core、内存为2048 MiB。

6.  在集群管理页左侧导航栏中，选择**配置管理** \> **配置项**。

7.  在配置项页面顶部选择**命名空间**为**kube-system**，单击**nginx-configuration****操作**列的**编辑**。

    ![配置项.png](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/8483522161/p237861.png)

8.  在**编辑**面板最下方单击**+添加**，设置**名称**为sentinel-params，**值**为--app=<应用名\>，然后单击**确定**。

    例如，本文示例的应用名为demo-k8s-2020，名称和值的设置如下：

    -   **名称**：sentinel-params。
    -   **值**：--app=demo-k8s-2020。
    ![设置应用名.png](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/8483522161/p237921.png)

    **说明：**

    -   如果您不配置AHAS的应用名，即不操作此步骤，则默认该应用名为ingress-sentinel-default。建议您自定义应用名，便于后期管理。
    -   sentinel-params与Nginx防护中sentinel\_sidecar\_run命令功能一致，更多信息，请参见[全局配置](/cn.zh-CN/流量防护/Nginx防护/Nginx Sentinel模块配置.md)。
9.  在**编辑**面板最下方单击**+添加**，设置**名称**为use-sentinel，**值**为true，然后单击**确定**。

    use-sentinel是流控开关配置项，表示是否加载流控组件：

    -   true：设置值为true后，表示加载流控组件，该配置项的值默认为true。
    -   false：设置值为false后，退化成不带流控功能的Ingress镜像，AHAS控制台的应用也会消失。

## 验证结果

1.  登录[AHAS控制台](https://ahas.console.aliyun.com)，然后在左上角选择**地域**。

    **说明：** 选择的地域要与步骤[1](#step_xlc_xlm_i3o)创建ACK集群的地域相同。

2.  在[AHAS控制台](https://ahas.console.aliyun.com)左侧导航栏选择**流量防护** \> **Nginx防护**。

    在Nginx防护页面，可以看到在[容器服务管理控制台](https://cs.console.aliyun.com)创建的应用，说明该Ingress已接入AHAS。

    ![AHAS控制台.png](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/8483522161/p237925.png)


接入Ingress后，可以为其配置流控规则。具体操作，请参见[配置流控规则](/cn.zh-CN/流量防护/Nginx防护/配置流控规则.md)。

