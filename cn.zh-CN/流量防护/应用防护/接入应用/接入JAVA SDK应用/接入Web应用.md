---
keyword: [Web应用防护, Web限流]
---

# 接入Web应用

将Web应用接入AHAS应用防护后，可以对其配置流控、降级和系统规则来保证系统稳定性。本文介绍如何使用SDK方式将Web应用接入应用防护。

## 操作步骤

1.  登录[AHAS控制台](https://ahas.console.aliyun.com/)。
2.  在AHAS控制台左上角，选择应用接入的**地域**。
3.  在控制台左侧导航栏中选择**流量防护** \> **应用防护**。
4.  在应用防护页面右上角单击**新应用接入**，然后在**JAVA语言**页签，单击**SDK接入**，单击**Web应用接入**。
5.  选择以下任意一种方式，在Web应用中添加应用防护依赖。
    -   在Web应用的Pom文件中添加以下依赖。

        ```
        <dependency>
          <groupId>com.alibaba.csp</groupId>
          <artifactId>ahas-sentinel-client</artifactId>
          <version>x.y.z</version>
        </dependency>
        ```

        在Web应用接入页面第一步：添加Pom依赖中查看Pom依赖最新版本，将`x.y.z`替换为新版本的版本号。

        ![WEB version1.png](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/5256725161/p246989.png)

    -   添加JAR包依赖。

        在**Web应用接入**页面单击**请点此链接下载**下载压缩包，并将压缩包中的所有JAR包放置在classpath目录下。

6.  在web.xml文件中引入拦截器，并将其配置为第一个Filter，示例如下。

    ```
    <filter>
        <filter-name>SentinelCommonFilter</filter-name>
        <filter-class>com.alibaba.csp.sentinel.adapter.servlet.CommonFilter</filter-class>
    </filter>
    
    <filter-mapping>
        <filter-name>SentinelCommonFilter</filter-name>
    <!-- 配置要拦截的URL模式。 -->
        <url-pattern>/*</url-pattern>
    </filter-mapping>
    ```

7.  配置应用的启动参数。

    若在公网地域，需要查看License信息。请在第三步：配置启动参数区域查看（非公网地域不需要），具体请参见[查看License](/cn.zh-CN/流量防护/应用防护/参考信息/查看License.md)。

    ![WEB license2.png](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/5256725161/p246990.png)

8.  您可以通过以下两种方式来设定自定义的跳转URL，当请求触发流控、降级或系统规则时会自动跳转至设定的URL。

    -   通过`WebServletConfig.setBlockPage(blockPage)`方法设定自定义的跳转URL。
    -   通过UrlBlockHandler接口编写定制化的限流处理逻辑，然后将其注册至WebCallbackManager中来实现，更多信息，请参见[Web Servlet Filter扩展接口](/cn.zh-CN/流量防护/应用防护/SDK 使用手册/扩展接口.md)。
    **说明：** 默认情况下，当请求触发流控、降级或系统规则时会返回默认提示页面，提示信息为：`Blocked by Sentinel (flow limiting)`。

9.  可以自定义URL清理，防止`/payment/{id}`这类REST风格的URL堆积过多影响系统性能，配置URL清理的方式有两种：
    -   实现自定义的UrlCleaner接口，自定义URL清理归一处理逻辑，请参见[Web Servlet Filter](https://help.aliyun.com/document_detail/102560.html#h2-url-1)。
    -   通过properties文件配置前缀清理。

        将properties文件中URL格式更改为：匹配前缀=清理后的资源名称，例如 /payment/=/payment/\*。再通过启动参数`-Dcsp.sentinel.url.clean.config.path`配置文件路径。

        **说明：** 启动参数中的默认路径为JAR包所在的ahas-sentinel-url-clean.properties文件。启动参数支持classpath形式，例如：`Dcsp.sentinel.url.clean.config.path=classpath:ahas-sentinel-url-clean.properties`。


## 结果验证

登录[AHAS控制台](https://ahas.console.aliyun.com)，在左侧导航栏选择**流量防护** \> **应用防护**，若在应用防护页面出现该应用的资源卡片且有数据上报，则说明接入成功。

![应用防护.png](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/1733858951/p139423.png)

