# 查看容器组（Kubernetes） {#concept_ub4_s3z_ngb .concept}

为 Kubernetes 应用安装 AHAS 探针后，AHAS 能自动识别系统中的 Pod、Deployment、Service 和它们与其他组件的依赖关系。

## 查看拓扑图 {#section_myn_2lz_ngb .section}

1.  登录 [AHAS 控制台](https://ahas.console.aliyun.com/)，从左侧导航栏选择**架构感知**。

2.  在架构感知页面，选择拓扑图左侧的**容器组**层，切换视图层次。拓扑图将显示当前环境中所有的容器组（默认显示 Pod 层架构信息）。

    在拓扑图上，可进行以下操作：

    -   **查看具体分层**：单击拓扑图左上角的 **Pod**、**Deployment**和 **Service**，可查看具体分层视图。
    -   **筛选**：在拓扑图上方的下拉列表中，可根据特定的 Kubernetes 集群、命名空间、状态等进行筛选。
    -   **切换至表格视图**：单击拓扑图右上角的**拓扑图**开关图标，可切换至表格视图。
    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/117706/155506311144340_zh-CN.png)

3.  在拓扑图上，单击某个图标，可查看对应的 Pod、Deployment 或 Service 的详情和具体拓扑图。

4.  （可选）单击页面右上角**拓扑图**切换图标，可查看 Pod、Deployment 和 Service 列表。在对应表头中，勾选筛选项或排序图标，可进行筛选或排序。
5.  当某容器组出现事件时，可以单击该容器组图标，查看其事件详情。具体事件说明，参见[事件列表](intl.zh-CN/架构感知/事件列表.md#)。

    ![](images/44344_zh-CN.png "容器事件")


## Pod 详情说明 {#section_g3x_tjg_4gb .section}

容器组中的 Pod 详情说明见下表（具体字段以实际接入的应用资源为准）。

|Pod 详情|说明|
|------|--|
|信息|命名空间（Namespace）|该 Pod 所在的命名空间|
|状态|该 Pod 的状态，包括： -   运行中（Running）
-   等待中（Pending）
-   正常退出（Succeeded）
-   非正常退出（Failed）
-   未知（Unknown）

 |
|创建时间（Uptime）|该 Pod 创建的时间|
|重启次数（Restart）|重启次数|
|IP|IP 地址|
|容器数量（Container Count）|该 Pod 包含的容器个数|
|标签|Name|N/A|
|POD-TEMPLATE-HASH|N/A|
|容器|该 Pod 相关联的容器，单击容器名称可跳转至容器详情。|
|进程|该 Pod 相关联的进程，单击进程名称可跳转至进程详情。|

## Deployment 详情说明 {#section_smg_lmg_4gb .section}

容器组中的 Deployment 详情说明见下表（具体字段以实际接入的应用资源为准）。

|Deployment 详情|说明|
|-------------|--|
|信息|命名空间（Namespace）|该 Deployment 所在的命名空间|
|类型（Type）|Deployment|
|创建时间|该 Deployment 创建的时间|
|副本数|N/A|
|就绪副本数|N/A|
|配置副本数|N/A|
|已更新副本数|N/A|
|ObservedGeneration|N/A|
|策略（Strategy）|N/A|
|容器数量（Container Count）|该 Deployment 包含的容器个数|
|标签|TASK|N/A|
|K8S-APP|N/A|
|容器组|该 Deployment 关联的容器组，单击容器组名称可跳转至容器组详情。|
|容器|该 Deployment 关联的容器，单击容器名称可跳转至容器详情。|
|进程|该 Deployment 关联的进程，单击进程名称可跳转至进程详情。|
|入口连接|调用该 Deployment 的所有组件及其端口；通过拓扑图中连接线的箭头方向可判断组件之间的调用关系。|
|出口连接|该 Deployment 调用的所有组件及其端口；通过拓扑图中连接线的箭头方向可判断组件之间的调用关系。|

|Service 详情|说明|
|----------|--|
|信息|命名空间（Namespace）|该 Service 所在的命名空间|
|类型（Type）|N/A|
|创建时间（Uptime）|该 Service 创建的时间|
|IP|IP 地址|
|Ports|端口|
|Selector|N/A|
|容器数量（Container Count）|该 Service 包含的容器个数|
|标签|Name|N/A|
|容器组|该 Service 相关联的容器组，单击容器组名称可跳转至容器组详情。|
|容器|该 Service 相关联的容器，单击容器名称可跳转至容器详情。|

