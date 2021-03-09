---
keyword: [MyBatis, ]
---

# 接入MyBatis应用

将MyBatis应用接入AHAS应用防护后，可以对其配置流控、降级和系统规则来保证系统稳定性。本文介绍使用SDK方式将MyBatis应用接入应用防护。

## 操作步骤

1.  登录[AHAS控制台](https://ahas.console.aliyun.com/)。
2.  在AHAS控制台左上角，选择应用接入的**地域**。
3.  在控制台左侧导航栏中选择**流量防护** \> **应用防护**。
4.  在应用防护页面右上角单击**新应用接入**。
5.  在**JAVA语言**页签，单击**SDK接入**，然后单击**Spring Boot应用接入**。
6.  通过以下任意一种方式，为应用添加依赖。
    -   方式一：在Pom文件中添加依赖：

        ```
        <dependency>
          <groupId>com.alibaba.csp</groupId>
          <artifactId>spring-boot-starter-ahas-sentinel-client</artifactId>
          <!-- 可指定版本号，最新版本见AHAS控制台应用防护应用接入页。 -->
          <version>x.y.z</version>
        </dependency>
        ```

        在Spring Boot应用接入页面第一步：添加Pom依赖中查看Pom依赖最新版本，将`x.y.z`替换为新版本的版本号。

        ![pom版本号.png](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/9156725161/p246957.png)

    -   方式二：添加JAR包依赖。
        1.  [下载ahas-sentinel依赖包](https://aliware-images.oss-cn-hangzhou.aliyuncs.com/ahas/ahas-sentinel.zip)。
        2.  解压依赖包，并将依赖包中的所有JAR包放置在classpath下。
7.  添加拦截器。
    -   若您使用了MyBatis Spring Boot Starter，则引入AHAS依赖后会自动接入（需要spring-boot-starter-ahas-sentinel-client 1.5.1及以上版本）。
    -   若您未使用MyBatis Spring Boot Starter，则需在MyBatis应用的XML配置文件中引入SentinelMyBatisMapperInterceptor拦截器依赖：

        ```
        <?xml version="1.0" encoding="UTF-8" ?>
        <!DOCTYPE configuration
                PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
                "http://mybatis.org/dtd/mybatis-3-config.dtd">
        <configuration>
            <plugins>
              <!-- 引入AHAS Sentinel拦截器 -->
                <plugin interceptor="com.alibaba.csp.sentinel.adapter.mybatis.SentinelMyBatisMapperInterceptor"/>
            </plugins>
        </configuration>
        ```

8.  通过以下任意一种方式，配置应用的启动参数。
    -   添加JVM -D参数。
    -   在application.properties文件中添加以下内容：

若在公网地域，需要查看License信息。请在Spring Boot应用接入页面查看（非公网地域不需要），具体请参见[查看License](/cn.zh-CN/流量防护/应用防护/参考信息/查看License.md)。

![Spring boot license2.png](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/9156725161/p246961.png)

## 结果验证

登录[AHAS控制台](https://ahas.console.aliyun.com)，在左侧导航栏选择**流量防护** \> **应用防护**，若在应用防护页面出现该应用的资源卡片且有数据上报，则说明接入成功。

![应用防护.png](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/1733858951/p139423.png)

## 后续操作

为应用配置流控降级规则请参见以下文档：

-   [配置流控规则](/cn.zh-CN/流量防护/应用防护/配置规则/配置流控规则.md)
-   [配置熔断规则](/cn.zh-CN/流量防护/应用防护/配置规则/配置熔断规则.md)
-   [自适应流控](/cn.zh-CN/流量防护/应用防护/配置规则/自适应流控.md)

当MyBatis应用触发配置的流控、降级或系统保护规则时，会抛出`MyBatisSentinelBlockException`类型的异常，您可以自行捕获该异常并进行处理。

