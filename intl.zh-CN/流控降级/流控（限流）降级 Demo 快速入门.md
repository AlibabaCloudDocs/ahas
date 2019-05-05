# 流控（限流）降级 Demo 快速入门 {#concept_101410_zh .concept}

AHAS 为您提供快速上手的流控（限流）降级样例工程（Demo），模拟访问请求等。只需运行 Demo 安装包即可快速接入 AHAS，查看 Demo 应用，体验流量控制、熔断降级的基本功能。

操作流程如下：

![](https://aliware-images.oss-cn-hangzhou.aliyuncs.com/ahas/dg_ahas-demo-flow.png)

**说明：** 流控降级样例工程（Demo）仅限体验限流、降级功能，不支持架构感知、故障演练的相关功能。

## 操作步骤 { .section}

1.  免费[开通 AHAS 服务](../../../../intl.zh-CN/准备工作/开通 AHAS.md#)。
2.  登录 [AHAS 控制台](https://ahas.console.aliyun.com)。

3.  在管理控制台最上方地域列表中，选择 Region：

-   如果您不确定如何选择 Region，可以选择 **公网**，作为样例工程运行环境；
-   如果您有阿里云北京、杭州、上海或深圳 VPC 的机器，可以选择对应的 Region。
4.  在左侧导航栏选择 **流控降级**，单击右上角 **添加应用**。

5.  选择**体验Demo**，查看 Demo 下载地址和对应的启动命令。

    1.  点击 [流控降级 Demo JAR 包](http://ahasoss-cn-hangzhou.oss-cn-hangzhou.aliyuncs.com/sdk/1.0.1/ahas-sentinel-sdk-demo.jar?file=ahas-sentinel-sdk-demo.jar)，进行下载。

    2.  在 Demo JAR 包所在目录，运行以下命令：

        -   如果您的机器在阿里云 VPC 网络的以下 Region 中：北京、杭州、上海或深圳，执行以下命令，APPName 可更改：
        ```
        java -Dproject.name=AppName -jar ahas-sentinel-sdk-demo.jar
        							
        ```

        -   如果您的机器不属于第一种情况，或者在本机运行 Demo，执行以下命令。APPName 可更改，License 需要您在过控制台**SDK 接入**引导页的 **体验Demo** 部分获取：
        ```
        java -Dproject.name=AppName -Dahas.license=<License> -jar ahas-sentinel-sdk-demo.jar
        							
        ```

6.  该样例工程为您构造应用及其访问请求。返回 AHAS 控制台的 **流控降级** 页面，查看 Demo 应用的数据。

    ![](https://aliware-images.oss-cn-hangzhou.aliyuncs.com/ahas/sc_demo_overview.png)

    单击该应用卡片，查看其资源详情。

    ![](https://aliware-images.oss-cn-hangzhou.aliyuncs.com/ahas/sc_demo_resource.png)

7.  您可以为该 Demo 应用创建流控、降级或系统规则，动态控制请求流量。下面以流控规则为例，操作如下：

    1.  在该应用的 **监控详情** 页面，单击某个资源卡片右上角的加号。
    2.  在 **新建规则** 窗口，以 QPS 作为流控指标，填写阈值（示例：5）。单击**新建**。

        ![](https://aliware-images.oss-cn-hangzhou.aliyuncs.com/ahas/dg_demo_resource_rules.png)

        在**监控详情**页面，观察该资源的 **通过QPS** 已从之前的 10 下降至 **5**，即流控规则已生效。

        ![](https://aliware-images.oss-cn-hangzhou.aliyuncs.com/ahas/dg_demo_resource_result.png)

    **说明：** 关于流控规则的更多说明，参考[流控规则](intl.zh-CN/流控降级/控制台指南/流控规则.md#)。


您也可以基于 Demo 应用进行更多操作：

-   [创建降级规则](intl.zh-CN/流控降级/控制台指南/降级规则.md#)
-   [创建系统规则](intl.zh-CN/流控降级/控制台指南/系统规则.md#)

