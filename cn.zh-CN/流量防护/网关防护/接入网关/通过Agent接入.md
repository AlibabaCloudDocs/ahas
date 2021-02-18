---
keyword: [网关防护, Agent接入]
---

# 通过Agent接入

若您的网关应用使用AHAS支持的第三方组件和框架，则可以使用Agent接入方式，无需修改代码即可接入AHAS应用防护。本文介绍如何通过Agent接入网关应用。

确认应用使用的第三方组件和框架在支持列表中，详细信息，请参见[支持组件列表](/cn.zh-CN/流量防护/应用防护/支持组件列表.md)。

## 操作步骤

1.  登录[AHAS控制台](https://ahas.console.aliyun.com)，然后在页面左上角选择**地域**。

2.  在控制台左侧导航栏中选择**流量防护** \> **网关防护**。

3.  在网关防护右上角单击**网关接入**。

4.  单击**Agent接入**页签。

5.  选择以下任意一种方式下载Agent。

    -   执行以下命令下载Agent。

        ```
        wget https://ahasoss-cn-hangzhou.oss-cn-hangzhou.aliyuncs.com/agent/prod/latest/ahas-java-agent.jar
        ```

    -   在页面，单击**此处链接下载**，下载ahas-java-agent.jar安装包。
6.  执行以下命令，启动应用并挂载Agent。

    若在公网地域，需要查看License信息。请在Agent接入页签查看（非公网地域不需要），具体操作，请参见[查看License](/cn.zh-CN/流量防护/应用防护/参考信息/查看License.md)。

    ![agent license.png](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/7222119951/p141317.png)

7.  重启网关。


## 结果验证

登录[AHAS控制台](https://ahas.console.aliyun.com)，在左侧导航栏选择**流量防护** \> **网关防护**，在网关防护页面出现该网关应用的资源卡片，则说明接入成功。

![网关防护.png](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/7222119951/p141032.png)

