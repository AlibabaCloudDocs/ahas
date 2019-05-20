# Spring Cloud Gateway 接入 {#concept_264107 .concept}

通过 SDK 接入的方式，将 Spring Cloud Gateway 接入 AHAS 控制台，使用流控降级服务。

## 操作步骤 {#section_m25_2fg_duy .section}

为 Spring Cloud Gateway 接入 AHAS 流控降级。

1.  在 Spring Cloud Gateway 服务的 pom.xml 文件中添加依赖：

    ``` {#codeblock_4yh_spv_1ja}
    <dependency>
        <groupId>com.alibaba.csp</groupId>
        <artifactId>spring-cloud-gateway-starter-ahas-sentinel</artifactId>
        <version>1.0.1</version>
    </dependency>
    ```

2.  通过以下任意一种方式，配置应用的启动参数。
    -   添加 JVM -D 参数

        ``` {#codeblock_myc_dub_mhl}
        #将 AppName 替换为自定义的应用名称。
        #通过**公网**地域接入时，需要您的证书信息；其他地域不需要证书。
        #证书获取方式：在 AHAS 控制台左侧导航栏，选择**流控降级 \> 网关流控**，选择右上角**网关接入**，在**配置启动参数**页签下，找到您的证书信息。
        -Dproject.name=AppName -Dahas.license=xxx
        ```

    -   修改 Spring Property 配置文件

        在 application.properties 文件添加以下内容：

        ``` {#codeblock_7b5_er2_2s7}
        #指定您要接入的特定的 AHAS 环境
        ahas.namespace=default
        #自定义您的应用名称，例如 spring-cloud-gateway
        project.name=spring-cloud-gateway
        #通过**公网**地域接入时，需要您的证书信息；其他地域不需要证书。
        #证书获取方式：在 AHAS 控制台左侧导航栏，选择**流控降级 \> 网关流控**，选择右上角**网关接入**，在**配置启动参数**页签下，找到您的证书信息。
        ahas.license=xxx
        ```

        接入配置完成后，需要网关有访问量，您才能在 AHAS 控制台的网关流控页面看到该网关服务。


