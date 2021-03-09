---
keyword: [接入HSF, JAVA SDK接入, HSF应用]
---

# 接入HSF应用

将HSF（高速服务框架，High-speed Service Framework）应用接入AHAS应用防护后，可以对其配置流控、降级和系统规则来保证系统稳定性。本文介绍如何使用SDK方式将HSF应用接入应用防护。

## 操作步骤

1.  登录[AHAS控制台](https://ahas.console.aliyun.com/)。
2.  在AHAS控制台左上角，选择应用接入的**地域**。
3.  在控制台左侧导航栏中选择**流量防护** \> **应用防护**。
4.  在应用防护页面右上角单击**新应用接入**。
5.  在**JAVA语言**页签，单击**SDK接入**，然后单击**Dubbo/HSF应用接入**。
6.  选择以下任意一种方式，在HSF应用中添加应用防护依赖。

    -   若是Spring Boot应用，则可以通过starter方式接入。在pom.xml中引入以下依赖：

        ```
        <dependency>
          <groupId>com.alibaba.csp</groupId>
          <artifactId>spring-boot-starter-ahas-sentinel-client</artifactId>
          <!-- 需指定版本号，需要≥1.7.2版本。最新版本见AHAS控制台应用防护新应用接入页引导。 -->
          <version>x.y.z</version>
        </dependency>
        ```

    -   若非Spring Boot应用，则在pom.xml中引入以下依赖：

        ```
        <dependency>
          <groupId>com.alibaba.csp</groupId>
          <artifactId>ahas-sentinel-client</artifactId>
          <!-- 需指定版本号，需要≥1.7.2 版本。最新版本见AHAS控制台应用防护新应用接入页引导。 -->
          <version>x.y.z</version>
        </dependency>
        ```

    在Dubbo/HSF接入页面第一步：添加Pom依赖中查看Pom依赖最新版本，将`x.y.z`替换为新版本的版本号。

    ![HSF接入1.png](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/7656725161/p246985.png)

7.  配置应用的启动参数。

    若在公网地域，需要查看License信息。请在第二步：添加埋点区域查看（非公网地域不需要），具体请参见[查看License](/cn.zh-CN/流量防护/应用防护/参考信息/查看License.md)。

    ![dubbo license2.png](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/7656725161/p246986.png)

8.  重启您的应用。
9.  您可以自定义HSF应用触发限流、降级或系统保护规则时的fallback处理逻辑，自定义HsfFallback接口并通过`HsfFallbackRegistry`注册即可（`setProviderFallback`针对服务提供方，`setConsumerFallback`针对服务消费方）。完成配置后，当HSF应用触发流控、降级或系统规则时，AHAS会将`BlockException`携带到fallback中。

    **说明：** 若未执行此步骤，当HSF应用触发应用防护规则时，默认抛出固定的异常`RuntimeException("SentinelBlockException")`。


## 结果验证

登录[AHAS控制台](https://ahas.console.aliyun.com)，在左侧导航栏选择**流量防护** \> **应用防护**，若在应用防护页面出现该应用的资源卡片且有数据上报，则说明接入成功。

![应用防护.png](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/1733858951/p139423.png)

