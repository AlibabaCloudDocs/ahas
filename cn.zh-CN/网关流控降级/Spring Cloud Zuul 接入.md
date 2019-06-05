# Spring Cloud Zuul 接入 {#concept_508450 .concept}

通过 SDK 接入的方式，将 Spring Cloud Zuul 应用接入 AHAS 控制台，使用流控降级服务。

## 操作步骤 {#section_3y1_053_ye6 .section}

1.  在您的 Spring Cloud Zuul 服务的 `pom.xml` 文件中添加依赖：

    ``` {#codeblock_eot_yp7_uxi}
    <dependency>
        <groupId>com.alibaba.csp</groupId>
        <artifactId>spring-cloud-zuul-starter-ahas-sentinel</artifactId>
        <version>1.0.1</version>
    </dependency>
    ```

2.  通过以下任意一种方式，配置应用的启动参数。
    -   添加 JVM -D 参数

        ``` {#codeblock_965_g6f_dki}
        # 将 AppName 替换为自定义的网关应用名称
        # 通过**公网**地域接入时，需要您的证书信息；其他地域不需要证书。
        # 证书获取方式：在 AHAS 控制台左侧导航栏选择**流控降级 \> 网关流控**，选择右上角**网关接入**，在**配置启动参数**页签下，找到您的 证书信息。
        -Dproject.name=AppName -Dahas.license=xxx
        ```

    -   修改 Spring Property 配置文件

        在 `application.properties` 文件添加以下内容：

        ``` {#codeblock_x0l_2sh_8uj}
        #指定您要接入的特定的 AHAS 环境
        ahas.namespace=default
        #自定义您的网关名称，比如这里叫 zuul-gateway
        project.name=zuul-gateway
        #通过公网地域接入时，需要您的证书信息；其他地域不需要证书。
        # 证书获取方式：在 AHAS 控制台左侧导航栏选择**流控降级 \> 网关流控**，选择右上角**网关接入**，在**配置启动参数**页签下，找到您的 证书信息。
        ahas.license=xxx
        ```

        接入配置完成后，需要网关有访问量，您才能在 AHAS 控制台的网关流控页面看到该网关服务。


