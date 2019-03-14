# Spring Cloud 应用接入 {#concept_iqr_c2z_bhb .concept}

通过 SDK 接入的方式，将 Spring Cloud 应用接入 AHAS 控制台，使用流控降级服务。目前 AHAS 提供 Java SDK。

**说明：** 关于 Java SDK 的常用 API，参见 [Java SDK 参考](../intl.zh-CN/流控降级/开发指南/Java SDK 参考/定义资源.md#)。

## 操作步骤 {#section_tbp_jhz_bhb .section}

为 Spring Boot 应用接入 AHAS 流控降级。

1.  在 pom.xml 文件中引入如下依赖：

    ```
    <dependency>
        <groupId>org.springframework.cloud</groupId>
        <artifactId>spring-cloud-alibaba-sentinel</artifactId>
      	<!-- 最新版本请参见 https://mvnrepository.com/artifact/org.springframework.cloud/spring-cloud-alibaba-sentinel -->
        <version>0.2.1.RELEASE</version>
    </dependency>
    
    <dependency>
      <groupId>com.alibaba.csp</groupId>
      <artifactId>spring-boot-starter-ahas-sentinel-client</artifactId>
      <!-- 可指定版本号，最新版本以 AHAS 控制台流控降级应用接入页引导为准。 -->
      <version>1.1.0</version>
    </dependency>
    ```

2.  若您需要修改拦截的 URL Pattern，需要在 Spring property 配置文件中进行配置。

    默认情况下，`spring-cloud-alibaba-sentinel`会对所有的 Web URL 资源进行统计，如下所示：

    ```
    spring.cloud.sentinel.filter.url-patterns=/*
    ```

    更多配置信息，请参见 [Spring Cloud Alibaba Sentinel 文档](https://github.com/spring-cloud-incubator/spring-cloud-alibaba/wiki/Sentinel)。

3.  通过以下任意一种方式，配置应用的启动参数。
    -   添加 JVM -D 参数

        ```
        //可修改 AppName 自定义您的应用名称
        //通过公网 Region 接入时，需要您的证书信息；其他地域不需要证书。
        //License 获取方式：在 AHAS 控制台左侧导航栏选择**流控降级**，选择右上角**应用接入**，在**配置启动参数**页签下，找到您的 License 信息。
        -Dproject.name=AppName -Dahas.license=xxx
        ```

    -   修改 Spring Property 配置文件

        在 application.properties 添加如下内容：

        ```
        #指定您要接入的特定的 AHAS 环境
        ahas.namespace=default
        #自定义您的应用名称
        project.name=AppName
        #通过公网 Region 接入时，需要您的证书信息；其他地域不需要证书。
        #License 获取方式：在 AHAS 控制台左侧导航栏选择**流控降级**，选择右上角**应用接入**，在**配置启动参数**页签下，找到您的 License 信息。
        ahas.license=xxx
        ```


