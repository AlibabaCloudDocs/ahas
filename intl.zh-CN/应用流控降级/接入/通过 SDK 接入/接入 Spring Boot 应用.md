# 接入 Spring Boot 应用 {#concept_bl5_lhq_bhb .concept}

将 Spring Boot 应用接入 AHAS 应用流控降级后，可以对其配置流控、降级和系统规则来保证系统稳定性。本文将帮助您了解如何使用 SDK 方式将 Spring Boot 应用接入应用流控降级。

## 操作步骤 {#section_cbd_g3q_bhb .section}

1.  登录 [AHAS 控制台](https://ahas.console.aliyun.com)，然后在页面左上角选择**地域**。
2.  在左侧导航栏中选择**流控降级** \> **应用流控**。
3.  在应用列表页面右上角单击**新应用接入**，然后选择**SDK 接入** \> **Spring Boot 应用接入**页签。

    在Spring Boot 应用接入 页面查看 Pom 依赖最新版本和 license 信息（非公网地域中不需要）。

    ![Spring boot 应用接入](images/59478_zh-CN.png "Spring boot 应用接入")

4.  在 Spring Boot 应用的 Pom 文件中引入依赖：

    ``` {#codeblock_b3s_3g7_myt}
    <dependency>
      <groupId>com.alibaba.csp</groupId>
      <artifactId>spring-boot-starter-ahas-sentinel-client</artifactId>
      <!-- 可指定版本号，最新版本见 AHAS 控制台流控降级应用接入页引导。 -->
      <version>x.y.z</version>
    </dependency>
    ```

    **说明：** 在Spring Boot 应用接入页签查看 Pom 依赖最新版本，将 `x.y.z` 替换为新版本的版本号。

5.  在应用工程中添加埋点
    -   添加 HTTP 埋点：

        ``` {#codeblock_dkn_9md_bnr}
        @Configuration
        public class SentinelWebConfig implements WebMvcConfigurer {
        
            @Override
            public void addInterceptors(InterceptorRegistry registry) {
                registry.addInterceptor(new SentinelWebInterceptor());
            }
        }
        ```

    -   添加自定义埋点：
        1.  配置 SentinelResourceAspect。

            ``` {#codeblock_jd7_1fy_beb}
            @Configuration
            public class SentinelAspectConfiguration {
              @Bean
              public SentinelResourceAspect sentinelResourceAspect() {
                return new SentinelResourceAspect();
              }
            }
            ```

        2.  在业务方法使用注解作为埋点。

            ``` {#codeblock_swp_jfb_6j0}
            @SentinelResource(value = "getUserById")
            public User getUserById(String id) {
              return new User(id);
            }
            ```

6.  通过以下任意一种方式，配置应用的启动参数。
    -   添加 JVM -D 参数。
    -   在 application.properties 添加以下内容：
7.  （可选）您可以自定义 Spring Boot 应用触发限流、降级或系统保护规则时的处理逻辑。

    -   若添加 HTTP 埋点，则使用 Web Servlet Filter 方式配置处理逻辑，参见[Web Servlet Filter](intl.zh-CN/应用流控降级/开发指南/配置流控逻辑.md#section_pgg_4vj_kgb)。
    -   若添加自定义埋点，则使用注解方式配置处理逻辑，参见[注解方式](intl.zh-CN/应用流控降级/开发指南/配置流控逻辑.md#section_kgg_4vj_kgb)。
    **说明：** 若未执行此步骤，当 Spring Boot 应用触发流控降级规则时，默认抛出 `BlockException` 异常类的子类（触发流控规则，则抛出流控异常 `FlowException`；触发降级规则，则抛出降级异常 `DegradeException`）。


## 结果验证 {#section_b0l_hge_mwc .section}

启动应用并调用配置埋点的方法。若该应用出现在 AHAS 控制台**流控降级** \> **应用流控**页面，且在该应用的监控详情页面有能看到配置埋点的方法，则说明接入成功。

## 后续操作 {#section_f5x_yxf_5pr .section}

为应用配置流控降级规则请参见以下文档：

-   [流控规则](intl.zh-CN/应用流控降级/控制台指南/流控规则.md#)
-   [降级规则](intl.zh-CN/应用流控降级/控制台指南/降级规则.md#)
-   [系统规则](intl.zh-CN/应用流控降级/控制台指南/系统规则.md#)

