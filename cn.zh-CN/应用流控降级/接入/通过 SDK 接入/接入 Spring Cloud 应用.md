# 接入 Spring Cloud 应用 {#concept_iqr_c2z_bhb .concept}

将 Spring Cloud 应用接入 AHAS 应用流控降级后，可以对其配置流控、降级和系统规则来保证系统稳定性。本文将帮助您了解如何使用 SDK 方式将 Spring Cloud 应用接入应用流控降级。

## 操作步骤 {#section_tbp_jhz_bhb .section}

为 Spring Boot 应用接入 AHAS 流控降级。

1.  在 pom.xml 文件中引入依赖：

    ``` {#codeblock_k9y_u2u_6wp}
    <dependency>
        <groupId>org.springframework.cloud</groupId>
        <artifactId>spring-cloud-alibaba-sentinel</artifactId>
      <!-- 最新版本请参见 https://mvnrepository.com/artifact/org.springframework.cloud/spring-cloud-alibaba-sentinel  -->  
        <version>0.2.1.RELEASE</version>
    </dependency>
    
    <dependency>
      <groupId>com.alibaba.csp</groupId>
      <artifactId>spring-boot-starter-ahas-sentinel-client</artifactId>
      <!-- 在 AHAS 控制台 > 流控降级 > 应用接入 > SDK 应用接入页签中查看最新版本信息。 -->
      <version>x.y.z</version>
    </dependency>+
    ```

2.  （可选）若需修改拦截的 URL Pattern，则需在 Spring property 配置文件中进行修改，参见[Spring Cloud Alibaba Sentinel](https://github.com/spring-cloud-incubator/spring-cloud-alibaba/wiki/Sentinel) 

    默认情况下，`spring-cloud-alibaba-sentinel`会对所有的 Web URL 资源进行统计，示例如下：

    ``` {#codeblock_l6m_69w_bwc}
    spring.cloud.sentinel.filter.url-patterns=/*
    ```

3.  通过以下任意一种方式，配置应用的启动参数。
    -   添加 JVM -D 参数。
    -   在 application.properties 添加以下内容：

## 结果验证 {#section_b0l_hge_mwc .section}

启动应用并调用配置埋点的方法。若该应用出现在 AHAS 控制台**流控降级** \> **应用流控**页面，且在该应用的监控详情页面有能看到配置埋点的方法，则说明接入成功。

## 后续操作 {#section_f5x_yxf_5pr .section}

为应用配置流控降级规则请参见以下文档：

-   [流控规则](intl.zh-CN/应用流控降级/控制台指南/流控规则.md#)
-   [降级规则](intl.zh-CN/应用流控降级/控制台指南/降级规则.md#)
-   [系统规则](intl.zh-CN/应用流控降级/控制台指南/系统规则.md#)

