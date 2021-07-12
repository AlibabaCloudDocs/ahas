---
keyword: [故障演练, 故障注入, Java进程]
---

# 如何排查Java场景下故障注入不生效的问题

在对Java进程注入故障时，可能会出现故障注入失败的情况。为解决此类问题，在创建或编辑演练时，您可以在故障执行阶段选择开启Debug模式，并通过相关的日志信息来了解故障注入失败的原因。

## 开启Debug模式

在查看目标演练的故障注入日志前，您需要先确认该演练的故障执行步骤是否已开启Debug模式。若未开启，可按照以下步骤设置目标演练的故障执行步骤，开启Debug模式。

1.  登录[AHAS控制台](https://ahas.console.aliyun.com)，在左侧导航栏选择**故障演练** \> **我的空间**。

2.  在我的空间页面，单击目标演练名称，进入目标演练的详情页。

3.  在**配置**页签下，单击**编辑演练**。

4.  在**演练内容**区域，单击故障执行步骤。

    ![故障执行步骤](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/4182175261/p292411.png)

5.  在右侧弹出的对话框的**开启DEBUG**区域，选择**开启**。

    ![开启Debug](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/4182175261/p292412.png)

6.  单击对话框底部的**关闭**，然后单击**保存**。


## 查看故障注入日志

1.  登录[AHAS控制台](https://ahas.console.aliyun.com)，在左侧导航栏选择**故障演练** \> **我的空间**。

2.  在我的空间页面，单击目标演练名称，进入目标演练的详情页。

3.  单击**演练记录**页签，然后在目标演练记录的**操作**列单击**查看详情**。

4.  在**执行情况**区域，单击故障执行节点，然后在右侧**机器**区域单击需要查看的机器地址。

    ![故障执行节点](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/4182175261/p292407.png)

5.  在弹出的对话框中，单击**故障注入日志**页签，查看故障执行的状态信息。

    若状态类型为INJECTION\_FAILURE，则表示故障执行失败。您可以通过**错误**区域显示的错误信息了解故障注入失败的原因。以下图为例，故障执行失败的原因是没有在脚本中找到类名。

    ![故障注入日志](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/4182175261/p292409.png)


