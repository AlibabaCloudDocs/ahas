---
keyword: [Kubernetes资源视图, K8s, Kubernetes集群]
---

# Kubernetes资源视图

为Kubernetes应用安装AHAS探针后，AHAS能自动识别系统中的Pod、Deployment、Service和它们与其他组件的依赖关系。通过采集Kubernetes元信息，构建Kubernetes资源的物理拓扑关系，支持自建Kubernetes集群、阿里云容器服务Kubernetes集群。

## 查看拓扑图

1.  登录[AHAS控制台](https://ahas.console.aliyun.com)，从左侧导航栏选择**架构感知** \> **架构地图**。

2.  在架构地图页面，单击Kubernetes监控视图的**查看视图**。进入Kubernetes资源视图页面。默认的拓扑图将显示当前环境中所有的容器组信息。

    **说明：** Kubernetes资源视图中只显示安装了AHAS探针的应用，若需要安装探针，请参见[管理探针](/cn.zh-CN/系统管理/管理探针.md)。

3.  单击页面右上角的**Kubernetes监控视图**，可进行以下操作。

    -   查看具体分层：在子视图中选择需要查看的具体分层视图，包括Node、Pod等，默认为Pod层架构信息。
    -   筛选：可根据特定的Kubernetes集群、命名空间、状态等进行筛选。
    ![子视图.png](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/6002635161/p127301.png)

4.  在拓扑图上，单击某个图标，可查看对应的信息、标签、容器等详情以及和其他产品的拓扑关系。在详情中，您可单击显示为链接的进程、容器或主机名，快速跳转至其详情，拓扑图也会随之变化。

    ![K8S](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/3752698951/p127557.png)


## 容器详情说明

容器参数详情如下表，其他参数信息请参见[列表信息](/cn.zh-CN/架构感知/参考信息/列表信息.md)。

|容器详情|说明|
|----|--|
|状态|CPU|该容器的CPU占有情况。|
|MEMORY|该容器的内存占有情况。|
|信息|ID|该容器的唯一标识符。|
|Name|容器名称。|
|State|状态。|
|Uptime|运行时间。|
|Restart|重启次数。|
|Networks|网络类型。|
|IPs|IP地址。|
|Ports|该容器的端口。|
|入网|调用该容器的所有容器及其端口；通过拓扑图中连接线的箭头方向可判断容器之间的调用关系。|
|出网|该容器调用的所有容器及其端口；通过拓扑图中连接线的箭头方向可判断容器之间的调用关系。|
|主机|该容器所在的主机，单击主机名称可跳转至主机详情。|

## Pod详情说明

容器组中的Pod详情说明见下表（具体字段以实际接入的应用资源为准），其他参数信息请参见[列表信息](/cn.zh-CN/架构感知/参考信息/列表信息.md)。

|Pod详情|说明|
|-----|--|
|信息|命名空间（Namespace）|该Pod所在的命名空间。|
|状态|该Pod的状态。 -   运行中（Running）
-   等待中（Pending）
-   正常退出（Succeeded）
-   非正常退出（Failed）
-   未知（Unknown） |
|创建时间（Uptime）|该Pod创建的时间。|
|重启次数（Restart）|重启次数。|
|IP|IP地址。|
|容器数量（Container Count）|该Pod包含的容器个数。|
|标签|Name|无|
|POD-TEMPLATE-HASH|无|
|容器|该Pod相关联的容器，单击容器名称可跳转至容器详情。|
|进程|该Pod相关联的进程，单击进程名称可跳转至进程详情。|

## Deployment详情说明

容器组中的Deployment详情说明见下表（具体字段以实际接入的应用资源为准），其他参数信息请参见[列表信息](/cn.zh-CN/架构感知/参考信息/列表信息.md)。

|Deployment详情|说明|
|------------|--|
|信息|命名空间（Namespace）|该Deployment所在的命名空间。|
|类型（Type）|Deployment。|
|创建时间|该Deployment创建的时间。|
|副本数|无|
|就绪副本数|无|
|配置副本数|无|
|已更新副本数|无|
|ObservedGeneration|无|
|策略（Strategy）|无|
|容器数量（Container Count）|该Deployment包含的容器个数。|
|标签|TASK|无|
|K8S-APP|无|
|容器组|该Deployment关联的容器组，单击容器组名称可跳转至容器组详情。|
|容器|该Deployment关联的容器，单击容器名称可跳转至容器详情。|
|进程|该Deployment关联的进程，单击进程名称可跳转至进程详情。|
|入网|调用该Deployment的所有组件及其端口；通过拓扑图中连接线的箭头方向可判断组件之间的调用关系。|
|出网|该Deployment调用的所有组件及其端口；通过拓扑图中连接线的箭头方向可判断组件之间的调用关系。|

## Service详情说明

容器组中的Service详情说明见下表（具体字段以实际接入的应用资源为准），其他参数信息请参见[列表信息](/cn.zh-CN/架构感知/参考信息/列表信息.md)。

|Service详情|说明|
|---------|--|
|信息|命名空间（Namespace）|该Service所在的命名空间。|
|类型（Type）|无|
|创建时间（Uptime）|该Service创建的时间。|
|IP|IP地址。|
|Ports|端口。|
|Selector|无|
|容器数量（Container Count）|该Service包含的容器个数。|
|标签|Name|无|
|容器组|该Service相关联的容器组，单击容器组名称可跳转至容器组详情。|
|容器|该Service相关联的容器，单击容器名称可跳转至容器详情。|

