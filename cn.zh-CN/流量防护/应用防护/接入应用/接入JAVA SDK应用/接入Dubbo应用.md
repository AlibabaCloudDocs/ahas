---
keyword: [Dubbo应用防护, JAVA SDK接入]
---

# 接入Dubbo应用

将Dubbo应用接入AHAS应用防护后，可以对其配置流控、降级和系统规则来保证系统稳定性。本文介绍如何使用SDK方式将Dubbo应用接入应用防护。

## 操作步骤

1.  登录[AHAS控制台](https://ahas.console.aliyun.com/)。
2.  在AHAS控制台左上角，选择应用接入的**地域**。
3.  在控制台左侧导航栏中选择**流量防护** \> **应用防护**。
4.  在应用防护页面右上角单击**新应用接入**。
5.  在**JAVA语言**页签，单击**SDK接入**，然后单击**Dubbo应用接入**。
6.  选择以下任意一种方式，在Dubbo应用中添加应用防护依赖。
    -   在Dubbo应用的Pom文件中添加以下依赖（默认支持Dubbo 2.6.x版本）：

        ```
        <dependency>
          <groupId>com.alibaba.csp</groupId>
          <artifactId>ahas-sentinel-client</artifactId>
          <!-- 可指定版本号，最新版本见AHAS控制台应用防护新应用接入页引导。 -->
          <version>x.y.z</version>
        </dependency>
        ```

        在Dubbo应用接入页面第一步：添加Pom依赖中查看Pom依赖最新版本，将`x.y.z`替换为新版本的版本号。

        ![Dubbo版本号2.png](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/8056725161/p246979.png)

        若您使用Dubbo 2.7.x版本，请添加以下依赖：

        ```
        <!-- SDK/Starter需1.6.2及以上版本，并排掉sentinel-dubbo-adapter依赖。 -->
        <dependency>
            <groupId>com.alibaba.csp</groupId>
            <artifactId>ahas-sentinel-client</artifactId>
            <version>1.6.2</version>
            <exclusions>
                <exclusion>
                    <groupId>com.alibaba.csp</groupId>
                    <artifactId>sentinel-dubbo-adapter</artifactId>
                </exclusion>
            </exclusions>
        </dependency>
        <!-- 使用开源2.7.x adapter依赖。-->
        <dependency>
            <groupId>com.alibaba.csp</groupId>
            <artifactId>sentinel-apache-dubbo-adapter</artifactId>
            <version>1.7.0</version>
            <exclusions>
                <exclusion>
                    <groupId>com.alibaba.csp</groupId>
                    <artifactId>sentinel-core</artifactId>
                </exclusion>
            </exclusions>
        </dependency>
        ```

    -   添加JAR包依赖。

        在Dubbo应用接入页面单击**请点此链接下载**下载压缩包，并将压缩包中的所有JAR包放置在classpath目录下。

7.  配置应用的启动参数。

    若在公网地域，需要查看License信息。请在第二步：添加埋点区域查看（非公网地域不需要），具体请参见[查看License](/cn.zh-CN/流量防护/应用防护/参考信息/查看License.md)。

    ![dubbo license2.png](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/8056725161/p246981.png)

8.  重启您的应用。
9.  您可以自定义Dubbo应用触发限流、降级或系统保护规则时的fallback处理逻辑，自定义[`DubboFallback`](https://github.com/alibaba/Sentinel/blob/master/sentinel-adapter/sentinel-dubbo-adapter/src/main/java/com/alibaba/csp/sentinel/adapter/dubbo/fallback/DubboFallback.java)接口并通过`DubboFallbackRegistry`注册即可。配置后，当Dubbo应用触发流控、降级或系统规则时，AHAS会将`BlockException`包装后抛出。更多信息，请参见[Dubbo Adapter](/cn.zh-CN/流量防护/应用防护/SDK 使用手册/配置触发规则后的逻辑.md)。

    **说明：** 若未执行此步骤，当Dubbo应用触发应用防护规则时，默认抛出`BlockException`异常类的子类（触发流控规则，则抛出流控异常`FlowException`；触发降级规则，则抛出降级异常`DegradeException`）。


## 结果验证

登录[AHAS控制台](https://ahas.console.aliyun.com)，在左侧导航栏选择**流量防护** \> **应用防护**，若在应用防护页面出现该应用的资源卡片且有数据上报，则说明接入成功。

![应用防护.png](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/1733858951/p139423.png)

