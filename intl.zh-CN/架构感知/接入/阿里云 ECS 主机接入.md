# 阿里云 ECS 主机接入 {#concept_xw3_z3y_ngb .concept}

通过一键安装 AHAS 探针，可快速将阿里云环境中的 ECS 主机（Linux）接入 AHAS 控制台，查看其系统架构、进行故障测评。

## 前提条件 {#section_hpc_5yy_ngb .section}

已开通 AHAS 服务，参见[开通 AHAS 服务](../../../../cn.zh-CN/准备工作/开通 AHAS.md#)。

## 选择地域 {#section_fdp_jky_ngb .section}

接入阿里云 VPC 网络的 Linux 主机前，需在控制台选择对应的地域。

1.  登录 [AHAS 控制台](https://ahas.console.aliyun.com/)。

2.  在控制台左上角，选择您的主机所在的地域。

    **说明：** 已开通的地域包括北京、杭州、上海、深圳，其他地域陆续开放中；目前，其他地域的阿里云 ECS 主机可以通过“公网”地域接入，接入方式可参考[普通 Linux 主机接入](cn.zh-CN/架构感知/接入/普通 Linux 主机接入.md#)。

3.  （可选）每个地域会有一个默认（Default）环境，您也可以添加自定义环境，如开发环境、测试环境等。
    1.  单击概览页面左上角的下拉列表，单击**添加环境**。

        ![](https://aliware-images.oss-cn-hangzhou.aliyuncs.com/ahas/sc_env_selection.png)

    2.  填写环境名称，单击**确定**。添加完成后，即可以在刚刚添加的环境中进行操作。

        如需切换，单击左上角下拉菜单，选择其他环境。


## 安装探针（地域：北京、杭州、上海或深圳） {#section_yyy_gjv_cgb .section}

按照下面的操作步骤为阿里云 ECS 主机安装应用高可用探针和 Java 探针，接入 AHAS 控制台。

1.  在 AHAS 控制台左侧导航栏，选择**探针管理**，单击页面右上角的**安装架构感知探针**。
2.  在**选择环境**页签下，单击**阿里云 ECS** 作为您要安装的环境。

    ![](https://aliware-images.oss-cn-hangzhou.aliyuncs.com/ahas/pg_wizard_1.png)

3.  在**安装应用高可用探针**页签下，列出了您账号下所有的 ECS 主机。按需执行以下操作之一，然后单击**下一步**。

    -   如需为单台主机安装探针，请单击右侧**操作**栏中的**单击安装**。
    -   如需为多台主机批量安装探针，请勾选目标主机左侧的复选框，并在页面左下角单击**批量安装**。
    ![](https://aliware-images.oss-cn-hangzhou.aliyuncs.com/ahas/pg_wizard_2.png)

4.  单击**下一步**，查看已安装的探针。
5.  单击**完成**。

    接入成功后，在 AHAS 控制台左侧导航栏，选择**架构感知**，将显示已接入应用的系统架构。


## 后续操作 {#section_sxn_k2z_ngb .section}

接入成功后，您可以执行操作：

-   [查看系统架构](cn.zh-CN/架构感知/查看系统架构.md#)
-   [测评应用的高可用能力](../../../../cn.zh-CN/故障演练/故障演练概述.md#)

