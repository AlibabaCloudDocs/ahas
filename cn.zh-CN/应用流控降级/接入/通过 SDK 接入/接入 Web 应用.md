# 接入 Web 应用 {#concept_t4z_mhq_bhb .concept}

将 Web 应用接入 AHAS 应用流控降级后，可以对其配置流控、降级和系统规则来保证系统稳定性。本文将帮助您了解如何使用 SDK 方式将 Web 应用接入应用流控降级。

## 操作步骤 {#section_h3x_rjq_bhb .section}

1.  登录 [AHAS 控制台](https://ahas.console.aliyun.com)，然后在页面左上角选择**地域**。
2.  在左侧导航栏中选择**流控降级** \> **应用流控**。
3.  在应用列表页面右上角单击**新应用接入**，然后选择**SDK 接入** \> **Web 应用接入**页签。

    在**Web 应用接入** 页面查看 Pom 依赖最新版本和 license 信息（非公网地域中不需要）。

    ![Web 应用接入](images/59481_zh-CN.png "Web 应用接入")

4.  选择以下任意一种方式，在 Dubbo 应用中添加应用流控降级依赖。
    -   在 Dubbo 应用的 Pom 文件中添加以下依赖：

        ``` {#codeblock_m9c_py2_3dj}
        <dependency>
          <groupId>com.alibaba.csp</groupId>
          <artifactId>ahas-sentinel-client</artifactId>
          <version>x.y.z</version>
        </dependency>
        ```

        **说明：** 在**Web 应用接入**页签查看 Pom 依赖最新版本，将 `x.y.z` 替换为新版本的版本号。

    -   添加 Jar 包依赖。

        在**Web 应用接入**页面单击**请点此链接下载**下载压缩包，并将压缩包中的所有 JAR 包放置在 classpath 目录下。

5.  在 web.xml 中引入拦截器，并将其配置为第一个 Filter，示例如下：

    ``` {#codeblock_2ll_rx2_gh4}
    <filter>
        <filter-name>SentinelCommonFilter</filter-name>
        <filter-class>com.alibaba.csp.sentinel.adapter.servlet.CommonFilter</filter-class>
    </filter>
    
    <filter-mapping>
        <filter-name>SentinelCommonFilter</filter-name    >
    //配置要拦截的 URL 模式
        <url-pattern>/*</url-pattern>
    </filter-mapping>
    ```

6.  通过以下任意一种方式，配置应用的启动参数。
    -   添加 JVM -D 参数。
    -   修改 Spring Property 配置文件。

        如果您正在使用 Spring，并且希望将配置写入 Spring Property 文件中，参照以下步骤：

        1.  在 pom.xml 中引入以下依赖：

            ``` {#codeblock_0sr_mcv_2vs}
            <dependency>
              <groupId>com.alibaba.csp</groupId>
              <artifactId>spring-boot-starter-ahas-sentinel-client</artifactId>
              <!-- 可指定版本号，最新版本见 AHAS 控制台流控降级应用接入页引导。 -->
              <version>x.y.z</version>
            </dependency>
            ```

            **说明：** 在Web 应用接入页签查看 Pom 依赖最新版本，将 `x.y.z` 替换为新版本的版本号。

        2.  在 application.properties 配置文件中，配置如下：
7.  （可选）您可以通过以下两种方式来设定自定义的跳转 URL，当请求被限流时会自动跳转至设定好的 URL。

    -   通过 `WebServletConfig.setBlockPage(blockPage)` 方法设定自定义的跳转 URL。
    -   通过 UrlBlockHandler 接口编写定制化的限流处理逻辑，然后将其注册至 WebCallbackManager 中来实现，详情可参见[Web Servlet Filter 扩展接口](intl.zh-CN/应用流控降级/开发指南/扩展接口.md#ul_epf_vfk_kgb)。
    **说明：** 默认情况下，当请求被限流时会返回默认的提示页面，提示信息为：`Blocked by Sentinel (flow limiting)。`

8.  （可选）可以自定义 URL 清理，防止 `/payment/{id}` 这类 REST 风格的 URL 堆积过多影响系统性能，配置 URL 清理的方式有两种：
    -   实现自定义的 UrlCleaner 接口，自定义 URL 清理归一处理逻辑，参见[Web Servlet Filter](https://help.aliyun.com/document_detail/102560.html#h2-url-1)。
    -   通过 properties 文件配置前缀清理。

        将 properties 文件中 URL 格式更改为：匹配前缀=清理后的资源名称，例如 /payment/=/payment/\*。再通过启动参数 `-Dcsp.sentinel.url.clean.config.path` 配置文件路径。

        **说明：** 启动参数中的默认路径为 JAR 包所在的 ahas-sentinel-url-clean.properties 文件。启动参数支持 classpath 形式，例如：`Dcsp.sentinel.url.clean.config.path=classpath:ahas-sentinel-url-clean.properties`。


## 结果验证 {#section_b0l_hge_mwc .section}

启动应用并调用配置埋点的方法。若应用出现在 AHAS 控制台**流控降级** \> **应用流控**页面，且在该应用的监控详情页面有能看到配置埋点的方法，则说明接入成功。

## 后续操作 {#section_f5x_yxf_5pr .section}

为应用配置流控降级规则请参见以下文档：

-   [流控规则](intl.zh-CN/应用流控降级/控制台指南/流控规则.md#)
-   [降级规则](intl.zh-CN/应用流控降级/控制台指南/降级规则.md#)
-   [系统规则](intl.zh-CN/应用流控降级/控制台指南/系统规则.md#)

