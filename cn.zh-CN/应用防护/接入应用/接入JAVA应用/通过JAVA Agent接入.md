# 通过JAVA Agent接入

若您的应用使用AHAS支持的第三方组件和框架，可使用Agent接入方式，零代码修改接入AHAS应用防护。本文以Java Agent为例介绍Agent接入方法。

## 前提条件

确认应用使用的第三方组件和框架在支持列表中，详情请参见[支持组件列表](/cn.zh-CN/应用防护/支持组件列表.md)。

## 操作步骤

1.  登录[AHAS控制台](https://ahas.console.aliyun.com/)。
2.  在AHAS控制台左上角，选择应用接入的**地域**。
3.  在控制台左侧导航栏中选择**流量防护** \> **应用防护**。
4.  在应用防护右上角单击**新应用接入**。
5.  在**JAVA语言**页签，单击**Agent接入**页签。
6.  按需选择以下一种方式安装并启动Java Agent。
    -   **方式一：快速接入**

        快速接入方式会识别主机中**所有Java进程**，并将其接入AHAS应用防护。

        1.  执行以下命令下载Java Agent。

            ```
            wget -O ./ahas-agent.sh https://ahasoss-cn-hangzhou.oss-cn-hangzhou.aliyuncs.com/agent/prod/latest/ahas-agent.sh
            ```

        2.  执行以下命令安装Java Agent。

            若在公网地域，需要查看License信息。请在第二步：安装Agent区域查看（非公网地域不需要），具体请参见[查看License](/cn.zh-CN/应用防护/参考信息/查看License.md)。

            ![license agent](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/9533858951/p110744.png)

        3.  重启您的应用。
    -   **方式二：手动接入**

        手动接入方式可以指定**单个应用**接入AHAS应用防护，操作时需要根据Java虚拟机运行的环境来安装Java Agent。

        1.  下载ahas-java-agent.jar安装包至任意路径下，例如：/opt/aliyunahas/agent。下载安装包请单击[ahas-java-agent.jar](https://ahasoss-cn-hangzhou.oss-cn-hangzhou.aliyuncs.com/agent/prod/latest/ahas-java-agent.jar)。
        2.  添加JVM启动参数。
        3.  启动JVM。

**说明：**

-   Agent接入配置URL收敛：通过启动参数`-Dcsp.sentinel.url.clean.config.path`配置文件路径，默认路径为jar包路径下的ahas-sentinel-url-clean.properties文件。支持classpath形式，如`-Dcsp.sentinel.url.clean.config.path=classpath:ahas-sentinel-url-clean.properties`。
-   Properties文件的格式：匹配前缀等于清理后的资源名称。
-   目前仅支持前缀匹配模式。如以下示例的配置会针对/payment/开头的URL，将它们归一成/payment/\*：`/payment/=/payment/*`。

## 结果验证

登录[AHAS控制台](https://ahas.console.aliyun.com)，在左侧导航栏选择**流量防护** \> **应用防护**，若在应用防护页面出现该应用的资源卡片且有数据上报，则说明接入成功。

![应用防护.png](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/1733858951/p139423.png)

## 常见问题

如果您已完成应用防护服务接入，应用防护页面仍查看不到您的应用，请参见[应用防护常见问题](/cn.zh-CN/常见问题/流量防护常见问题.md)。



