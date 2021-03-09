---
keyword: [Serverless应用引擎, SAE平台, SAE应用防护]
---

# 接入SAE应用

对于在Serverless应用引擎SAE（Serverless App Engine）平台上部署的应用，可以使用AHAS应用防护对其配置流控、隔离等规则来保证系统稳定性。本文介绍如何将SAE平台上的应用接入AHAS应用防护。

您已在SAE平台部署应用，具体操作，请参见[应用部署](/cn.zh-CN/应用部署/应用部署概述.md)。

SAE是面向应用的Serverless PaaS平台，能够帮助PaaS层用户免运维IaaS、按需使用、按量计费，从而轻松实现微服务应用上云。相对于其他Serverless产品，SAE抽象了应用的概念，并提供了一整套微服务解决方案，支持Spring Cloud、Dubbo、HSF等主流的微服务开发框架，实现了Serverless架构和微服务架构的完美结合。

## 操作步骤

1.  登录[AHAS控制台](https://ahas.console.aliyun.com)，然后在页面左上角选择**地域**。

2.  在控制台左侧导航栏中选择**流量防护** \> **应用防护**。

3.  在应用防护页面右上角单击**新应用接入**。然后在**JAVA语言**页签下，单击**SAE接入**。

4.  配置启动参数，添加JVM -D参数。

    ```
    -Dahas.namespace=default -Dproject.name=<AppName> -Dahas.license=<your license>
    ```

    注意事项如下：

    -   `<AppName>`只能包含字母、数字、下划线（\_）、短划线（-）、英文句号（.）以及英文冒号（:）。
    -   请将`<AppName>`参数替换成您的应用名。
    -   请将`<your license>`替换成应用防护控制台界面实际显示的license。

        ![SAE license2.png](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/9556725161/p246949.png)


## 结果验证

登录[AHAS控制台](https://ahas.console.aliyun.com)，在左侧导航栏选择**流量防护** \> **应用防护**，若在应用防护页面出现该应用的资源卡片且有数据上报，则说明接入成功。

![应用防护.png](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/1733858951/p139423.png)

