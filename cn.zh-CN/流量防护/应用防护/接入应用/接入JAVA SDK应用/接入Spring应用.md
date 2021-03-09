---
keyword: [Spring应用, 注解埋点, Spring应用防护]
---

# 接入Spring应用

通过在业务逻辑上添加依赖注解的方式将Spring应用接入应用防护，可以对调用方法进行注解埋点，减小对代码的入侵。本文将介绍如何将Spring应用接入应用防护。

## 操作步骤

1.  登录[AHAS控制台](https://ahas.console.aliyun.com/)。
2.  在AHAS控制台左上角，选择应用接入的**地域**。
3.  在控制台左侧导航栏中选择**流量防护** \> **应用防护**。
4.  在应用防护页面右上角单击**新应用接入**，然后在**JAVA语言**页签，单击**SDK接入**，然后单击**Spring应用接入**。
5.  通过以下任意一种方式，为应用添加依赖。
    -   方式一：在Pom文件中添加依赖。

        ```
        <dependency>
          <groupId>com.alibaba.csp</groupId>
          <artifactId>ahas-sentinel-client</artifactId>
          <version>x.y.x</version>
        </dependency>
        ```

        在Spring应用接入页面第一步：添加Pom依赖中查看Pom依赖最新版本，将`x.y.z`替换为新版本的版本号。

        ![pom版本号2.png](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/5356725161/p246963.png)

    -   方式二：添加JAR包依赖。

        在Spring应用接入页面单击**请点击此链接下载**下载压缩包，并将压缩包中的所有JAR包解压后放置在classpath目录下。

6.  在应用工程中添加埋点。
    -   添加HTTP埋点。

        ```
        @Configuration
        public class SentinelWebConfig implements WebMvcConfigurer {
          @Override
          public void addInterceptors(InterceptorRegistry registry) {
            registry.addInterceptor(new SentinelWebInterceptor());
          }
        }
        ```

    -   普通接口埋点。
        1.  将SentinelResourceAspect注册为一个Spring Bean。

            ```
            @Configuration
            public class SentinelAspectConfiguration {
              @Bean
              public SentinelResourceAspect sentinelResourceAspect() {
                return new SentinelResourceAspect();
              }
            }
            ```

        2.  在业务方法上添加@SentinelResource注解。

            ```
            // 原本的业务方法
            @SentinelResource(value = "getUserById")
            public User getUserById(String id) {
              return new User(id);
            }
            ```

7.  通过以下任意一种方式，配置应用的启动参数。

    若在公网地域，需要查看License信息。请在第三步：配置启动参数区域查看（非公网地域不需要），具体请参见[查看License](/cn.zh-CN/流量防护/应用防护/参考信息/查看License.md)。

    ![Spring license2.png](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/5356725161/p246966.png)

8.  重启应用。
9.  使用注解方式配置应用触发限流、降级或系统保护规则时的处理逻辑。 请参见[注解方式](/cn.zh-CN/流量防护/应用防护/SDK 使用手册/配置触发规则后的逻辑.md)。

    **说明：** 若未执行此步骤，当应用触发流控降级规则时，默认抛出`BlockException`异常类的子类（触发流控规则，则抛出流控异常`FlowException`；触发降级规则，则抛出降级异常`DegradeException`）。


## 结果验证

登录[AHAS控制台](https://ahas.console.aliyun.com)，在左侧导航栏选择**流量防护** \> **应用防护**，若在应用防护页面出现该应用的资源卡片且有数据上报，则说明接入成功。

![应用防护.png](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/1733858951/p139423.png)

