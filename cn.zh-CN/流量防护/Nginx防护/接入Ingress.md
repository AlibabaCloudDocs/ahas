---
keyword: [Ingress Nginx, ACK, Nginx防护]
---

# 接入Ingress

Ingress是Kubernetes中的一个资源对象，用来管理集群外部访问集群内部服务的方式。AHAS支持Ingress接入Nginx防护，然后对其设置流控规则，实现应用的高可用。本文介绍如何接入Ingress。

-   [开通AHAS](/cn.zh-CN/快速入门/开通AHAS.md)。
-   [创建Kubernetes托管版集群](/cn.zh-CN/Kubernetes集群用户指南/集群/创建集群/创建Kubernetes托管版集群.md)。

    在创建ACK集群时，必须选中**安装Ingress组件**。

    ![安装Ingress组件.png](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/7483522161/p237763.png)

-   请确保ACK集群中的Ingress Controller运行正常，且不低于0.44.0版本。

## 开启Ingress-sentinel流控功能

1.  在[容器服务管理控制台](https://cs.console.aliyun.com)左侧导航栏中，单击**集群**。然后在集群列表页面中，单击目标集群名称或者目标集群右侧**操作**列下的**详情**。

2.  在集群管理页左侧导航栏中，选择**工作负载** \> **无状态**。

3.  在无状态页面顶部选择**命名空间**为**kube-system**，在无状态列表搜索并单击**nginx-ingress-controller**的**操作**列的**编辑**。

    ![替换镜像.png](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/7483522161/p237832.png)

4.  在编辑页面，单击**nginx-ingress-controller**页签，设置以下参数，然后单击**更新**。

    设置**所需资源**的**CPU**为**1000m** Core，**内存**为**2048** MiB。其他参数保持默认设置。

    **说明：** 由于引入流控功能会带来一些资源消耗，所以建议您设置Ingress最小配置CPU为1000m Core、内存为2048 MiB。

5.  在集群管理页左侧导航栏中，选择**配置管理** \> **配置项**。

6.  在配置项页面顶部选择**命名空间**为**kube-system**，单击并搜索**nginx-configuration**的**操作**列的**编辑**。

    ![配置项.png](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/8483522161/p237861.png)

7.  在**编辑**面板最下方单击**+添加**，设置相关参数，然后单击**确定**。

    -   设置**名称**为sentinel-params。
    -   设置**值**请参考以下方式：
        -   若应用是在深圳、北京、上海、张家口、杭州五个地域，设置**值**为--app=<应用名\>。
        -   若应用是在其他地域，设置**值**为--app=<应用名\> --license=<license\>。实际<license\>的获取方式，请参见[查看License](/cn.zh-CN/流量防护/应用防护/参考信息/查看License.md)。
    例如，本文示例的应用名为demo-k8s-2020，名称和值的设置如下：

    -   **名称**：sentinel-params。
    -   **值**的设置分为两种情况：
        -   若应用是在深圳、北京、上海、张家口、杭州五个地域，设置**值**为--app=demo-k8s-2020。

            ![公共云](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/8691946161/p254183.png)

        -   若应用是在其他地域，设置**值**为--app=demo-k8s-2020 --license=<license\>。

            ![其他地域](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/8691946161/p254184.png)

    **说明：**

    -   如果您不配置AHAS的应用名，即不操作此步骤，则默认该应用名为ingress-sentinel-default。建议您自定义应用名，便于后期管理。
    -   sentinel-params与Nginx防护中sentinel\_sidecar\_run命令功能一致，更多信息，请参见[全局配置](/cn.zh-CN/流量防护/Nginx防护/Nginx Sentinel模块配置.md)。
8.  在**编辑**面板最下方单击**+添加**，设置**名称**为use-sentinel，**值**为true，然后单击**确定**。

    use-sentinel是流控开关配置项，表示是否加载流控组件：

    -   true：设置值为true后，表示加载流控组件，该配置项的值默认为false。
    -   false：设置值为false后，退化成不带流控功能的Ingress镜像，AHAS控制台的应用也会消失。

## 验证结果

1.  登录[AHAS控制台](https://ahas.console.aliyun.com)，然后在左上角选择**地域**。

    **说明：** 选择的地域要与创建ACK集群的地域相同。

2.  在[AHAS控制台](https://ahas.console.aliyun.com)左侧导航栏选择**流量防护** \> **Ingress/Nginx防护**。

    在Ingress/Nginx防护页面，可以看到在[容器服务管理控制台](https://cs.console.aliyun.com)创建的应用，说明该Ingress已接入AHAS。

    ![AHAS控制台2.png](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/0787725161/p247031.png)


接入Ingress后，可以为其配置流控规则。具体操作，请参见[配置流控规则](/cn.zh-CN/流量防护/Nginx防护/配置流控规则.md)。

