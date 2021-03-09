---
keyword: [流控, 接入, Spring Boot, SDK, Spring Cloud]
---

# 接入Spring Boot/Spring Cloud应用

将Spring Boot/Spring Cloud应用接入AHAS应用防护后，可以对其配置流控、隔离、熔断、系统或热点规则来保证系统稳定性。本文介绍如何使用SDK方式将Spring Boot/Spring Cloud应用接入应用防护。

## 操作步骤

1.  登录[AHAS控制台](https://ahas.console.aliyun.com/)。
2.  在AHAS控制台左上角，选择应用接入的**地域**。
3.  在控制台左侧导航栏中选择**流量防护** \> **应用防护**。
4.  在应用防护页面右上角单击**新应用接入**。
5.  在**JAVA语言**页签，单击**SDK接入**，然后单击**Spring Boot应用接入**。
6.  在Spring Boot应用的Pom文件中引入依赖。

    ```
    <dependency>
      <groupId>com.alibaba.csp</groupId>
      <artifactId>spring-boot-starter-ahas-sentinel-client</artifactId>
      <!-- 可指定版本号，最新版本见AHAS控制台流量防护新应用接入页。-->
      <version>x.y.z</version>
    </dependency>
    ```

    在Spring Boot应用接入页面第一步：添加Pom依赖中查看Pom依赖最新版本，将`x.y.z`替换为新版本的版本号。

    ![pom版本号.png](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/9156725161/p246957.png)

7.  在应用工程中添加埋点。
    -   添加HTTP埋点：引入spring-boot-starter-ahas-sentinel-client依赖后，应用会自动添加Web接口埋点。

        **说明：**

        -   若您从1.5.1之前的版本升级到1.5.1+版本，或额外引入了Web filter等的bean，需要先将之前注册bean的相关代码去掉，否则可能会导致重复统计。
        -   注解方式blockHandler和fallback函数的方法签名有限制，具体信息，请参见[注解方式](/cn.zh-CN/流量防护/应用防护/SDK 使用手册/配置触发规则后的逻辑.mdsection_kgg_4vj_kgb)。
        -   1.8.0及以上版本注解方式埋点支持自动重试规则。
    -   添加MyBatis SQL埋点：
        -   若您使用了MyBatis Spring Boot Starter，则引入AHAS依赖后会自动识别DAO埋点（需要spring-boot-starter-ahas-sentinel-client 1.5.1及以上版本）。
        -   若您未使用MyBatis Spring Boot Starter ，则需在MyBatis应用的XML配置文件中引入SentinelMyBatisMapperInterceptor拦截器依赖。

            ```
            <?xml version="1.0" encoding="UTF-8" ?>
            <!DOCTYPE configuration
                    PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
                    "http://mybatis.org/dtd/mybatis-3-config.dtd">
            <configuration>
                <plugins>
                  <!-- 引入AHAS Sentinel拦截器。 -->
                    <plugin interceptor="com.alibaba.csp.sentinel.adapter.mybatis.SentinelMyBatisMapperInterceptor"/>
                </plugins>
            </configuration>
            ```

    -   添加普通接口埋点（注解方式）：
        1.  引入[spring-boot-starter-aop](https://mvnrepository.com/artifact/org.springframework.boot/spring-boot-starter-aop?spm=a2c4g.11186623.2.12.72b64256UAFhnC)。

            **说明：** 若您的工程中已引入此依赖，则跳过此步骤。

        2.  在业务方法使用注解作为埋点。

            若不配置BlockHandler，则被流控降级时方法会直接抛出BlockException，若方法未定义Throws BlockException则会被JVM包装一层UndeclaredThrowableException。BlockHandler和Fallback函数的方法签名有限制，详情请参见[配置触发规则后的逻辑](/cn.zh-CN/流量防护/应用防护/SDK 使用手册/配置触发规则后的逻辑.md)。

            ```
            @SentinelResource(value = "getUserById")
            public User getUserById(String id) {
              return new User(id);
            }
            ```

    -   添加Feign埋点：引入Starter依赖后，在application.properties文件中配置`feign.sentinel.enabled`即可。Feign埋点的资源名格式为`feign:${httpMethod}:${url}`，例如`feign:http://localhost:8088/hello`。

        **说明：** spring-boot-starter-ahas-sentinel-client 1.8.4及以上版本支持。

8.  通过以下任意一种方式，配置应用的启动参数。
    -   添加JVM -D参数。
    -   在application.properties文件中添加以下内容：

        若在公网地域，需要查看License信息。请在第三步：配置启动参数区域查看（非公网地域不需要），具体请参见[查看License](/cn.zh-CN/流量防护/应用防护/参考信息/查看License.md)。

        ![Spring boot license2.png](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/9156725161/p246961.png)

9.  您可以自定义Spring Boot应用触发限流、降级或系统保护规则时的处理逻辑。

    -   若添加HTTP埋点，则使用Web Servlet Filter方式配置处理逻辑。具体操作，请参见[Web Servlet Filter](/cn.zh-CN/流量防护/应用防护/SDK 使用手册/配置触发规则后的逻辑.mdsection_pgg_4vj_kgb)。
    -   若添加自定义埋点，则使用注解方式配置处理逻辑。具体操作，请参见[注解方式](/cn.zh-CN/流量防护/应用防护/SDK 使用手册/配置触发规则后的逻辑.mdsection_kgg_4vj_kgb)。
    **说明：** 若未执行此步骤，当Web接口触发流控降级规则时，返回默认的提示信息（状态码为429）；注解方式接口默认抛出BlockException异常类的子类（触发流控规则，则抛出流控异常FlowException；触发降级规则，则抛出降级异常DegradeException），若方法未定义throws BlockException则会被JVM包装一层UndeclaredThrowableException。


## 结果验证

登录[AHAS控制台](https://ahas.console.aliyun.com)，在左侧导航栏选择**流量防护** \> **应用防护**，若在应用防护页面出现该应用的资源卡片且有数据上报，则说明接入成功。

![应用防护.png](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/1733858951/p139423.png)

