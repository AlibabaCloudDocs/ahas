# 普通 Linux 主机接入 {#concept_vvp_1jy_ngb .concept}

除了阿里云 ECS 和 Kubernetes 主机外，您可以通过手动安装探针的方式将任意厂商的 Linux 主机接入应用高可用服务 AHAS。

只要您的主机有公网连接，即可接入 AHAS 控制台，使用架构感知、故障演练功能。

## 前提条件 {#section_hpc_5yy_ngb .section}

已[开通 AHAS 服务](../intl.zh-CN/准备工作/开通 AHAS.md#)。

## 选择地域 {#section_fdp_jky_ngb .section}

接入 Linux 主机前，在控制台选择地域：**公网**。

1.  登录 [AHAS 控制台](https://ahas.console.aliyun.com/)。

2.  在控制台左上角，选择**公网**。
3.  （可选）每个地域会有一个默认（Default）环境，您也可以添加自定义环境，如开发环境、测试环境等。
    1.  单击概览页面左上角的下拉列表，单击**添加环境**。

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/92853/155955551047674_zh-CN.png)

    2.  填写环境名称，单击**确定**。添加完成后，即可以在刚刚添加的环境中进行操作。

        如需切换，单击左上角下拉列表，选择其他环境。


## 安装探针（地域：公网） {#section_dzl_4qh_dgb .section}

当您在地域列表中选择了**公网**，按照以下步骤安装应用高可用探针和 Java 探针。

1.  在 AHAS 控制台左侧导航栏，选择**探针管理**，单击页面右上角的**安装架构感知探针**。
2.  在选择环境页签下，单击您要安装的环境。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/92853/155955551147678_zh-CN.png)

3.  在**安装应用高可用探针**页签下，建议您按照页面上的提示操作。

    **说明：** 在安装探针的过程中，需要使用 License。在控制台页面的命令行中，已经自动分配了您的 License。

    如果您按照本文中的步骤操作，请在控制台页面找到您的 License 并带入到以下命令行的 License 变量中。

    登陆主机，使用 root 用户执行以下命令：

    **说明：** license 替换为控制台命令行提示中的 license。

    ```
    wget -q https://ahasoss-cn-public.oss-cn-hangzhou.aliyuncs.com/agent/prod/aliyunahasctl.sh  -O /tmp/aliyunahasctl.sh && sh /tmp/aliyunahasctl.sh install -e prod -s public -k <license\> -r cn-public -n default
    					
    ```

4.  单击**下一步**，查看已安装的探针。
5.  单击**完成**。

    接入成功后，在 AHAS 控制台左侧导航栏，选择**架构感知**，将显示已接入应用的系统架构。


## 后续操作 {#section_sxn_k2z_ngb .section}

接入成功后，您可以执行操作：

-   [查看系统架构](intl.zh-CN/架构感知/查看系统架构.md#)
-   [测评应用的高可用能力](../intl.zh-CN/故障演练/故障演练概述.md#)

