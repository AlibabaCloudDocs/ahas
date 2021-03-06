---
keyword: [接入层, MSFE, 同城多活]
---

# 配置MSFE

接入层主要是一个基于Tengine的多活组件，简称为MSFE。MSFE需要多单元部署，它能承接所有的单元前端流量，并按照路由规则路由到正确单元的后端应用。多活控制台提供MSFE集群新建、扩容、缩容等常规运维能力。本文介绍如何配置MSFE。

[新建命名空间](/cn.zh-CN/多活容灾/用户指南/同城多活配置/新建命名空间.md)

## 操作步骤

1.  登录[AHAS控制台](https://ahas.console.aliyun.com)。

2.  在控制台左侧导航栏中选择**多活容灾**。

3.  在左侧导航栏选择**同城多活** \> **MSFE配置**，然后在顶部选择命名空间。

4.  在MSFE配置页面，单击**新增域名**，并在**设置域名详情**面板进行以下配置。

    可以选择通过域名或IP任意一种方式接入。

    -   **接入类型**选择**域名**。
        1.  编辑域名。

            **说明：** 编辑域名时需先确认Zone域名，例如chinatax.test，然后在每个中心的DNS控制台中创建该全局Zone域名后才能使用，否则页面会提示错误。

            填写域名后，**单元子域名**区域将自动生成每个单元下的子域名。

        2.  选择**域名解析类型**。
            -   DNS解析：阿里云DNS请选择DNS解析。
            -   不解析：如果DNS不是阿里云DNS，是其它供应商，请选择**不解析**。
        3.  选择**多单元解析**。
            -   是：为每个单元生成子域名，异地双活和异地双读场景必选，同城多活场景可选。
            -   否：不为每个单元生成子域名，同城多活场景可选。
        4.  从**证书**列表选择所需证书。

            若没有证书，请单击**配置证书**，并在**域名证书配置**对话框中配置参数，然后单击**确定**。如果接入域名不是HTTPS域名，此项可空。

        5.  选择**纠错类型**。
            -   **反向代理**：Upstream，将非本单元的请求跨单元代理到正确单元的应用SLB中。
            -   **重定向**：Redirect，将非本单元的请求重定向到正确单元的子域名中。在单元间网络不通的情况下，只能使用301，但是301会造成浏览器域名变化与页面刷新，不建议使用。
        6.  选择**生效集群**。
        7.  单击**确定**。
    -   **接入类型**选择**IP**。
        1.  输入需要接入的IP地址，这个IP是单元的Frontend Service对外提供的IP。
        2.  选择**纠错类型**。
            -   **反向代理**：将非本单元的请求跨单元代理到正确单元的应用SLB中。
            -   **重定向**：将非本单元的请求重定向到正确单元的子域名中。在单元间网络不通的情况下，只能使用301，但是301会造成浏览器域名变化与页面刷新，不建议使用。
        3.  从**协议**下拉列表中选择协议。
        4.  选择**生效集群**。
        5.  单击**确定**。
    配置完成后，新增域名将出现在MSFE配置页面的域名列表中。

    ![同城接入层.png](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/2318683061/p177157.png)

5.  在目标域名右侧**配置**栏单击**生效**。

    域名以及URI的修改，必须单击**生效**才会真实生效。执行生效操作后，可以在该域名**配置规则**列查看状态，在**最近一次任务**列单击**查看**，可以查看生效任务详情。

6.  在目标域名右侧**配置**栏按需还可以进行以下配置。

    -   **修改**：修改域名配置信息。
    -   **URI**：新增、修改、删除URI。
        -   新增URI：在配置URI面板中单击**添加**，然后按需配置**URI**等信息，单击**确定**。**回源应用**信息的输入格式为IP:PORT，多个**回源应用**用英文逗号（,）相隔。
        -   修改URI：在配置URI面板中单击目标URI右侧的**修改**，然后按需修改**URI**等信息，单击**确定**。
        -   删除URI：在配置URI面板中单击目标URI右侧的**删除**，在删除对话框中单击**确认**。

