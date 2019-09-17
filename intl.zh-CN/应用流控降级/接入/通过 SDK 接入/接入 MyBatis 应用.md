# 接入 MyBatis 应用 {#concept_2229939 .concept}

将 MyBatis 应用接入 AHAS 应用流控降级后，可以对其配置流控、降级和系统规则来保证系统稳定性。本文将帮助您了解如何使用 SDK 方式将 MyBatis 应用接入应用流控降级。

## 操作步骤 {#section_pw4_ovz_2mc .section}

1.  通过以下任意一种方式，为应用添加依赖。
    -   方式一：在 Pom 文件中添加依赖：

        ``` {#codeblock_tky_if8_ekn}
        <dependency>
          <groupId>com.alibaba.csp</groupId>
          <artifactId>ahas-sentinel-client</artifactId>
          <version>x.y.x</version>
        </dependency>
        ```

        **说明：** 在 AHAS 控制台**流控降级** \> **应用接入** \> **SDK 应用接入**页签查看 Pom 依赖最新版本，将 `x.y.z` 替换为新版本的版本号。

    -   方式二：添加 JAR 包依赖。
        1.  [下载 ahas-sentinel 依赖包](https://aliware-images.oss-cn-hangzhou.aliyuncs.com/ahas/ahas-sentinel.zip) 。
        2.  解压压缩包，将压缩包中的所有 JAR 包放置在 classpath 下。
2.  在 MyBatis 应用的 xml 配置文件中添加 SentinelMyBatisInterceptor 拦截器配置。

    ``` {#codeblock_4t7_evw_cxl}
    <?xml version="1.0" encoding="UTF-8" ?>
    <!DOCTYPE configuration
            PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
            "http://mybatis.org/dtd/mybatis-3-config.dtd">
    <configuration>
        <plugins>
          <!-- 引入 AHAS Sentinel 拦截器 -->
            <plugin interceptor="com.alibaba.csp.sentinel.demo.db.mybatis.interceptor.SentinelMyBatisInterceptor"/>
        </plugins>
    </configuration>
    ```

3.  通过以下任意一种方式，配置应用的启动参数。
    -   添加 JVM -D 参数。
    -   修改 Spring Property 配置文件。

        如果您正在使用 Spring，并且希望将配置写入 Spring Property 文件中，参照以下步骤：

        1.  在 pom.xml 中引入以下依赖：

            ``` {#codeblock_e2c_i26_pwb}
            <dependency>
              <groupId>com.alibaba.csp</groupId>
              <artifactId>spring-boot-starter-ahas-sentinel-client</artifactId>
              <!-- 可指定版本号，最新版本见 AHAS 控制台流控降级应用接入页引导。 -->
              <version>x.y.z</version>
            </dependency>
            ```

            **说明：** 在Dubbo 应用接入页签查看 Pom 依赖最新版本，将 `x.y.z` 替换为新版本的版本号。

        2.  在 application.properties 配置文件中，配置如下：
4.  （可选）对应的 SQL 被流控降级后，会抛出 `MyBatisSentinelBlockException` 类型的异常，您可以自行捕获该异常并进行处理。

## 结果验证 {#section_b0l_hge_mwc .section}

启动应用并调用配置埋点的方法。若应用出现在 AHAS 控制台**流控降级** \> **应用流控**页面，且在该应用的监控详情页面有能看到配置埋点的方法，则说明接入成功。

## 后续操作 {#section_f5x_yxf_5pr .section}

为应用配置流控降级规则请参见以下文档：

-   [流控规则](intl.zh-CN/应用流控降级/控制台指南/流控规则.md#)
-   [降级规则](intl.zh-CN/应用流控降级/控制台指南/降级规则.md#)
-   [系统规则](intl.zh-CN/应用流控降级/控制台指南/系统规则.md#)

