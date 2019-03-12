# 通过 SDK 接入 {#concept_gz5_d3c_kgb .concept}

您可以通过 SDK 接入的方式，将应用接入 AHAS 控制台，使用流控降级服务。目前 AHAS 提供 Java SDK，支持 Dubbo、Spring Boot、Spring Cloud 等主流框架的适配，并支持通过手动接入方式，进行应用接入。

根据应用的实际情况，选择一种方式进行接入：

-   [Dubbo 应用接入](intl.zh-CN/流控降级/接入/通过 SDK 接入.md#section_ry5_m4d_bhb)
-   [Spring Boot/Spring Cloud 应用接入](intl.zh-CN/流控降级/接入/通过 SDK 接入.md#section_vdg_r4d_bhb)
-   [Web 应用接入](intl.zh-CN/流控降级/接入/通过 SDK 接入.md#section_pjh_q4d_bhb)
-   [通过 API 接入](intl.zh-CN/流控降级/接入/通过 SDK 接入.md#section_dlm_s4d_bhb)
-   [通过注解接入](intl.zh-CN/流控降级/接入/通过 SDK 接入.md#section_f3k_t4d_bhb)

**说明：** 关于 Java SDK 的常用 API，参见 [Java SDK 参考](intl.zh-CN/流控降级/开发指南/Java SDK 参考/定义资源.md#)。

## 基本流程 {#section_mqn_zjd_ggb .section}

应用接入的具体方式不同，但都遵循以下基本流程。

![](https://aliware-images.oss-cn-hangzhou.aliyuncs.com/ahas/dg_ahas_sentinel_access_workflow.png) 

## Dubbo 应用接入 {#section_ry5_m4d_bhb .section}

为 Dubbo 应用引入依赖包后，即可接入并自动定义资源，无需额外配置。

1.  通过以下任意一种方式，为应用添加依赖。
    -   方式一（推荐）：在 pom.xml 文件中引入如下依赖：

        ```
        <dependency>
          <groupId>com.alibaba.csp</groupId>
          <artifactId>ahas-sentinel-client</artifactId>
          //可指定版本号，最新版本以 AHAS 控制台流控降级应用接入页引导为准。
          <version>1.1.0</version>
        </dependency>
        ```

    -   方式二：添加 JAR 包依赖。
        1.  [下载 ahas-sentinel 依赖包](http://ahasoss-cn-hangzhou.oss-cn-hangzhou.aliyuncs.com/sdk/1.1.0/ahas-sentinel.zip?spm=5176.11961263.SystemGuard.8.769e3bc1c6ehKR&file=ahas-sentinel.zip) 。
        2.  解压压缩包，将压缩包中的所有 JAR 包到放置在 classpath 下，引入即可。
2.  通过以下任意一种方式，配置应用的启动参数。
    -   添加 JVM -D 参数

        ```
        //可修改 AppName 自定义您的应用名称
        //通过公网 Region 接入时，需要您的证书信息；其他地域不需要证书。
        //License 获取方式：在 AHAS 控制台左侧导航栏选择**流控降级**，选择右上角**应用接入**，在**配置启动参数**页签下，找到您的 License 信息。
        -Dproject.name=AppName -Dahas.license=xxx
        ```

    -   修改 Spring Property 配置文件

        如果您正在使用 Spring，并且希望将配置写入 Spring Property 文件中，参照以下步骤：

        1.  在 pom.xml 中引入如下依赖：

            ```
            <dependency>
              <groupId>com.alibaba.csp</groupId>
              <artifactId>spring-boot-starter-ahas-sentinel-client</artifactId>
              //可指定版本号，最新版本以 AHAS 控制台流控降级应用接入页引导为准。
              <version>1.1.0</version>
            </dependency>
            ```

        2.  在 application.properties 配置文件中，进行如下配置：

            ```
            //可指定您要接入的特定的 AHAS 环境
            ahas.namespace=default
            //可自定义您的应用名称
            project.name=AppName
            //通过公网 Region 接入时，需要您的证书信息；其他地域不需要证书。
            //License 获取方式：在 AHAS 控制台左侧导航栏选择**流控降级**，选择右上角**应用接入**，在**配置启动参数**页签下，找到您的 License 信息。
            ahas.license=xxx
            ```


应用接入配置完成后，需要应用有访问量，您才能在 AHAS 控制台的流控降级页面看到该应用卡片。

## Spring Boot/Spring Cloud 应用接入 {#section_vdg_r4d_bhb .section}

为 Spring Boot/Spring Cloud 应用接入 AHAS 流控降级。

1.  通过以下任意一种方式，为应用添加依赖。
    -   方式一（推荐）：在 pom.xml 文件中引入如下依赖：

        ```
        <dependency>
          <groupId>com.alibaba.csp</groupId>
          <artifactId>ahas-sentinel-client</artifactId>
          //可指定版本号，最新版本以 AHAS 控制台流控降级应用接入页引导为准。
          <version>1.1.0</version>
        </dependency>
        ```

    -   方式二：添加 JAR 包依赖。
        1.  [下载 ahas-sentinel 依赖包](http://ahasoss-cn-hangzhou.oss-cn-hangzhou.aliyuncs.com/sdk/1.1.0/ahas-sentinel.zip?spm=5176.11961263.SystemGuard.8.769e3bc1c6ehKR&file=ahas-sentinel.zip) 。
        2.  解压压缩包，将压缩包中的所有 JAR 包到放置在 classpath 下，引入即可。
2.  在应用工程中加入如下类：

    ```
    @Configuration
    public class WebConfig {
      @Bean
      public FilterRegistrationBean sentinelFilterRegistration() {
        FilterRegistrationBean registration = new FilterRegistrationBean();
        registration.setFilter(new CommonFilter());
        //请根据实际情况，定义哪些 UrlPatterns 适用该类。
    	registration.addUrlPatterns("*.json","*.hml","*.html","/demo/*");
        registration.setName("sentinelCommonFilter");   registration.setOrder(1);
        return registration;
      }
    }
    ```

3.  通过以下任意一种方式，配置应用的启动参数。
    -   添加 JVM -D 参数

        ```
        //可修改 AppName 自定义您的应用名称
        //通过公网 Region 接入时，需要您的证书信息；其他地域不需要证书。
        //License 获取方式：在 AHAS 控制台左侧导航栏选择**流控降级**，选择右上角**应用接入**，在**配置启动参数**页签下，找到您的 License 信息。
        -Dproject.name=AppName -Dahas.license=xxx
        ```

    -   修改 Spring Property 配置文件

        如果您正在使用 Spring，并且希望将配置写入 Spring Property 文件中，参照以下步骤：

        1.  在 pom.xml 中引入如下依赖：

            ```
            <dependency>
              <groupId>com.alibaba.csp</groupId>
              <artifactId>spring-boot-starter-ahas-sentinel-client</artifactId>
              //可指定版本号，最新版本以 AHAS 控制台流控降级应用接入页引导为准。
              <version>1.1.0</version>
            </dependency>
            ```

        2.  在 application.properties 配置文件中，进行如下配置：

            ```
            //可指定您要接入的特定的 AHAS 环境
            ahas.namespace=default
            //可自定义您的应用名称
            project.name=AppName
            //通过公网 Region 接入时，需要您的证书信息；其他地域不需要证书。
            //License 获取方式：在 AHAS 控制台左侧导航栏选择**流控降级**，选择右上角**应用接入**，在**配置启动参数**页签下，找到您的 License 信息。
            ahas.license=xxx
            ```


应用接入配置完成后，需要应用有访问量，您才能在 AHAS 控制台的流控降级页面看到该应用卡片。

## Web 应用接入 {#section_pjh_q4d_bhb .section}

为 Web 应用接入 AHAS 流控降级。

1.  通过以下任意一种方式，为应用添加依赖。
    -   方式一（推荐）：在 pom.xml 文件中引入如下依赖：

        ```
        <dependency>
          <groupId>com.alibaba.csp</groupId>
          <artifactId>ahas-sentinel-client</artifactId>
          //可指定版本号，最新版本以 AHAS 控制台流控降级应用接入页引导为准。
          <version>1.1.0</version>
        </dependency>
        ```

    -   方式二：添加 JAR 包依赖。
        1.  [下载 ahas-sentinel 依赖包](http://ahasoss-cn-hangzhou.oss-cn-hangzhou.aliyuncs.com/sdk/1.1.0/ahas-sentinel.zip?spm=5176.11961263.SystemGuard.8.769e3bc1c6ehKR&file=ahas-sentinel.zip) 。
        2.  解压压缩包，将压缩包中的所有 JAR 包到放置在 classpath 下，引入即可。
2.  在 web.xml 中引入 CommonFilter，并将其配置为第一个 Filter，示例如下：

    ```
    <filter>
      //引入 CommonFilter，并将其配置为第一个 Filter
      <filter-name>CommonFilter</filter-name>
      <filter-class>com.alibaba.csp.sentinel.adapter.servlet.CommonFilter</filter-class>
    </filter>
    //定义哪些资源使用上面配置的 CommonFilter。请根据实际情况，调整 url-pattern。
    <filter-mapping>
      <filter-name>CommonFilter</filter-name>
      <url-pattern>*.htm</url-pattern>
    </filter-mapping>
    <filter-mapping>
      <filter-name>CommonFilter</filter-name>
      <url-pattern>*.html</url-pattern>
    </filter-mapping>
    <filter-mapping>
      <filter-name>CommonFilter</filter-name>
      <url-pattern>*.do</url-pattern>
    </filter-mapping>
    ```

3.  通过以下任意一种方式，配置应用的启动参数。
    -   添加 JVM -D 参数

        ```
        //可修改 AppName 自定义您的应用名称
        //通过公网 Region 接入时，需要您的证书信息；其他地域不需要证书。
        //License 获取方式：在 AHAS 控制台左侧导航栏选择**流控降级**，选择右上角**应用接入**，在**配置启动参数**页签下，找到您的 License 信息。
        -Dproject.name=AppName -Dahas.license=xxx
        ```

    -   修改 Spring Property 配置文件

        如果您正在使用 Spring，并且希望将配置写入 Spring Property 文件中，参照以下步骤：

        1.  在 pom.xml 中引入如下依赖：

            ```
            <dependency>
              <groupId>com.alibaba.csp</groupId>
              <artifactId>spring-boot-starter-ahas-sentinel-client</artifactId>
              //可指定版本号，最新版本以 AHAS 控制台流控降级应用接入页引导为准。
              <version>1.1.0</version>
            </dependency>
            ```

        2.  在 application.properties 配置文件中，进行如下配置：

            ```
            //可指定您要接入的特定的 AHAS 环境
            ahas.namespace=default
            //可自定义您的应用名称
            project.name=AppName
            //通过公网 Region 接入时，需要您的证书信息；其他地域不需要证书。
            //License 获取方式：在 AHAS 控制台左侧导航栏选择**流控降级**，选择右上角**应用接入**，在**配置启动参数**页签下，找到您的 License 信息。
            ahas.license=xxx
            ```


应用接入配置完成后，需要应用有访问量，您才能在 AHAS 控制台的流控降级页面看到该应用卡片。

## 通过 API 接入 {#section_dlm_s4d_bhb .section}

通过定义 API 的方式，为应用接入 AHAS 流控降级。

1.  通过以下任意一种方式，为应用添加依赖。
    -   方式一（推荐）：在 pom.xml 文件中引入如下依赖：

        ```
        <dependency>
          <groupId>com.alibaba.csp</groupId>
          <artifactId>ahas-sentinel-client</artifactId>
          //可指定版本号，最新版本以 AHAS 控制台流控降级应用接入页引导为准。
          <version>1.1.0</version>
        </dependency>
        ```

    -   方式二：添加 JAR 包依赖。
        1.  [下载 ahas-sentinel 依赖包](http://ahasoss-cn-hangzhou.oss-cn-hangzhou.aliyuncs.com/sdk/1.1.0/ahas-sentinel.zip?spm=5176.11961263.SystemGuard.8.769e3bc1c6ehKR&file=ahas-sentinel.zip) 。
        2.  解压压缩包，将压缩包中的所有 JAR 包到放置在 classpath 下，引入即可。
2.  使用如下代码包住您的业务逻辑：

    ```
    Entry entry = null;
    try { 
      //保护业务逻辑
      entry = SphU.entry("HelloWorld"); 
      System.out.println("hello world");
    } catch (BlockException e) {
      //处理拦截逻辑
    } finally {
      //请确保 exit() 逻辑在此处被调用。 
      if (entry != null) {
        entry.exit();
      }
    }t();
      }
    }
    ```

3.  通过以下任意一种方式，配置应用的启动参数。
    -   添加 JVM -D 参数

        ```
        //可修改 AppName 自定义您的应用名称
        //通过公网 Region 接入时，需要您的证书信息；其他地域不需要证书。
        //License 获取方式：在 AHAS 控制台左侧导航栏选择**流控降级**，选择右上角**应用接入**，在**配置启动参数**页签下，找到您的 License 信息。
        -Dproject.name=AppName -Dahas.license=xxx
        ```

    -   修改 Spring Property 配置文件

        如果您正在使用 Spring，并且希望将配置写入 Spring Property 文件中，参照以下步骤：

        1.  在 pom.xml 中引入如下依赖：

            ```
            <dependency>
              <groupId>com.alibaba.csp</groupId>
              <artifactId>spring-boot-starter-ahas-sentinel-client</artifactId>
              //可指定版本号，最新版本以 AHAS 控制台流控降级应用接入页引导为准。
              <version>1.1.0</version>
            </dependency>
            ```

        2.  在 application.properties 配置文件中，进行如下配置：

            ```
            //可指定您要接入的特定的 AHAS 环境
            ahas.namespace=default
            //可自定义您的应用名称
            project.name=AppName
            //通过公网 Region 接入时，需要您的证书信息；其他地域不需要证书。
            //License 获取方式：在 AHAS 控制台左侧导航栏选择**流控降级**，选择右上角**应用接入**，在**配置启动参数**页签下，找到您的 License 信息。
            ahas.license=xxx
            ```


应用接入配置完成后，需要应用有访问量，您才能在 AHAS 控制台的流控降级页面看到该应用卡片。

## 通过注解接入 {#section_f3k_t4d_bhb .section}

在业务逻辑上添加注解，为应用接入 AHAS 流控降级。

1.  通过以下任意一种方式，为应用添加依赖。
    -   方式一（推荐）：在 pom.xml 文件中引入如下依赖：

        ```
        <dependency>
          <groupId>com.alibaba.csp</groupId>
          <artifactId>ahas-sentinel-client</artifactId>
          //可指定版本号，最新版本以 AHAS 控制台流控降级应用接入页引导为准。
          <version>1.1.0</version>
        </dependency>
        ```

    -   方式二：添加 JAR 包依赖。
        1.  [下载 ahas-sentinel 依赖包](http://ahasoss-cn-hangzhou.oss-cn-hangzhou.aliyuncs.com/sdk/1.1.0/ahas-sentinel.zip?spm=5176.11961263.SystemGuard.8.769e3bc1c6ehKR&file=ahas-sentinel.zip) 。
        2.  解压压缩包，将压缩包中的所有 JAR 包到放置在 classpath 下，引入即可。
2.  通常我们会结合 Spring AOP 使用注解特性，您需要引入 Spring AOP 的相关依赖。

-   非 Spring Boot 应用可以引入 [spring-aop](https://mvnrepository.com/artifact/org.springframework.boot/spring-boot-starter-aop)：选择版本，可查看对应的引入代码示例。
-   Spring Boot 或 Spring Cloud 应用可以引入 [spring-boot-starter-aop](https://mvnrepository.com/artifact/org.springframework.boot/spring-boot-starter-aop)：选择版本，可查看对应的引入代码示例。
3.  通过配置的方式将 SentinelResourceAspect 注册为一个 Spring Bean：

    ```
    @Configuration
    public class SentinelAspectConfiguration {
      @Bean
      public SentinelResourceAspect sentinelResourceAspect() {
        return new SentinelResourceAspect();
      }
    }
    ```

4.  在业务方法上添加 @SentinelResource 注解：

    ```
    // 原本的业务方法
    @SentinelResource(value = "getUserById")
    public User getUserById(String id) {
      return new User(id);
    }
    ```

    您也可以在注解上配置 blockHandler 和 fallback 函数，用于处理方法被限流、降级时的情况。更多指引，请参见 [Sentinel 注解支持文档](https://github.com/alibaba/Sentinel/wiki/%E6%B3%A8%E8%A7%A3%E6%94%AF%E6%8C%81)。

5.  通过以下任意一种方式，配置应用的启动参数。
    -   添加 JVM -D 参数

        ```
        //可修改 AppName 自定义您的应用名称
        //通过公网 Region 接入时，需要您的证书信息；其他地域不需要证书。
        //License 获取方式：在 AHAS 控制台左侧导航栏选择**流控降级**，选择右上角**应用接入**，在**配置启动参数**页签下，找到您的 License 信息。
        -Dproject.name=AppName -Dahas.license=xxx
        ```

    -   修改 Spring Property 配置文件

        如果您正在使用 Spring，并且希望将配置写入 Spring Property 文件中，参照以下步骤：

        1.  在 pom.xml 中引入如下依赖：

            ```
            <dependency>
              <groupId>com.alibaba.csp</groupId>
              <artifactId>spring-boot-starter-ahas-sentinel-client</artifactId>
              //可指定版本号，最新版本以 AHAS 控制台流控降级应用接入页引导为准。
              <version>1.1.0</version>
            </dependency>
            ```

        2.  在 application.properties 配置文件中，进行如下配置：

            ```
            //可指定您要接入的特定的 AHAS 环境
            ahas.namespace=default
            //可自定义您的应用名称
            project.name=AppName
            //通过公网 Region 接入时，需要您的证书信息；其他地域不需要证书。
            //License 获取方式：在 AHAS 控制台左侧导航栏选择**流控降级**，选择右上角**应用接入**，在**配置启动参数**页签下，找到您的 License 信息。
            ahas.license=xxx
            ```


应用接入配置完成后，需要应用有访问量，您才能在 AHAS 控制台的流控降级页面看到该应用卡片。

## 后续操作 {#section_ckr_l2j_kgb .section}

接入了 AHAS 的流控降级服务后，您可以进一步了解：

-    [实时监控应用数据](..md) 
-    [流控规则](..md) 
-    [降级规则](..md) 
-    [系统规则](..md) 

## 常见问题 {#section_umj_m2j_kgb .section}

如果您已完成流控降级服务接入，流控降级页面仍查看不到您的应用，可参考常见问题：[流控降级页面找不到应用](..md)。

