# Java SDK和Java Agent版本说明

本文记录了Java SDK和Java Agent的版本发布说明。

## 版本说明

本文包含以下Java SDK和Java Agent版本说明：

-   [Java SDK](#section_1d8_oqe_fxm)
    -   [AHAS-Sentinel-Client版本说明](#table_94i_ijr_ov9)
    -   [Spring-Boot-Starter-AHAS-Sentinel-Client版本说明](#table_qfc_18b_g2f)
    -   [Spring-Cloud-Gateway-Starter-AHAS-Sentinel版本说明](#table_289_pbg_r4n)
    -   [Spring-Cloud-Zuul-Starter-AHAS-Sentinel版本说明](#table_7vl_s14_8hf)
-   [Java Agent](#table_2id_vp3_3i0)

## Java SDK

**AHAS-Sentinel-Client版本说明**

|版本号|发布时间|版本说明|
|---|----|----|
|1.8.9|2021年04月09日|新增上海金融云环境支持。|
|1.8.8|2021年04月02日|-   新增自适应流控采样日志。
-   完善HSF adapter判断本机调用及解析来源的逻辑。 |
|1.8.7|2021年03月12日|修复Web fallback自定义返回文本包含中文时会出现乱码的问题。|
|1.8.6|2021年02月05日|-   集群流控支持自动调整单机退化阈值。
-   完善对Apache Dubbo 2.7.1~2.7.3版本的支持。 |
|1.8.5|2021年02月01日|支持VPC环境内的MST压测。|
|1.8.4|2021年01月28日|-   新增主动降级规则，针对Servlet、Spring Web、Spring Cloud Gateway的主动降级规则支持配置自定义降级行为。
-   完善MyBatis DAO埋点支持的场景。 |
|1.8.3|2021年01月13日|-   修复HTTP状态码统计模块线程池满时抛出异常的问题。

**说明：** 建议1.8.x旧版本至少升级至此版本。

-   支持通过启动参数指定全局滑动窗口配置。 |
|1.8.2|2021年01月09日|-   完善日志管理、清除逻辑。
-   完善对Dubbo 2.7.x版本的支持（无需额外引入依赖）。 |
|1.8.1|2020年12月23日|-   修复HTTP、状态码统计模块可能导致CPU被占满的问题。
-   支持通过sentinel.properties文件配置AHAS license、namespace。 |
|1.8.0|2020年12月16日|-   新增自动重试规则，新增SentinelWrapper托管调用埋点方式。目前SentinelWrapper埋点、注解埋点及HTTP Client适配支持自动重试规则。
-   新增HTTP接口状态码统计，支持Spring Web、Spring Cloud Gateway、Zuul 1.x。
-   新增指标统计，操作系统指标新增内存、网络、磁盘等指标种类；JVM指标新增GC、JVM内存、线程数等指标。 |
|1.7.5|2020年12月07日|支持与AHAS Sentinel Java Agent同时使用，SDK在探测到Agent相关类存在时不会触发初始化，Web、MyBatis等相关适配模块不会重复生效。|
|1.7.3|2020年11月03日|修复熔断降级模块在同资源配置多个规则时可能出现无法从half-open状态中恢复的问题。|
|1.7.2|2020年10月20日|-   新增支持HSF适配模块，原生支持接入EDAS HSF服务。
-   控制台监控支持区分各个埋点的流量类型（入口流量/出口流量/内部调用）。 |
|1.7.1|2020年09月25日|-   改进CPU使用率自适应流控策略，提高容器环境下获取CPU使用率的准确性。
-   新增一键自适应流控开关。 |
|1.7.0|2020年09月03日|AHAS SDK公有云和专有云版本统一。|
|1.6.6|2020年08月28日|修复Spring Web适配在内部forward请求的场景下可能会导致统计错误的问题。|
|1.6.5|2020年08月07日|-   修复部分阈值配置下匀速排队模式间隔时间控制不准确的问题。
-   Web适配模块默认流控逻辑支持自定义CORS配置。 |
|1.6.4|2020年07月17日|-   集群流控支持单机大流量场景（批量请求）。
-   修复熔断降级规则阈值比例为100%时不生效的问题。 |
|1.6.3|2020年06月12日|-   注解方式支持void返回的fallback/defaultFallback，支持配置全局统一的fallback。
-   优化集群流控。 |
|1.6.2|2020年05月28日|熔断降级新增渐进式恢复策略。|
|1.6.1|2020年04月29日|支持VPC环境通过license绑定用户。|
|1.6.0|2020年04月24日|-   改进熔断降级特性：引入半开启探测模式，支持任意统计时长，RT模式改进为慢调用比例模式。
-   优化集群流控通信与异常处理。
-   支持张家口region。
-   优化日志依赖。 |
|1.5.5|2020年04月14日|修复在不支持的region即使配了license也不会走公网的问题。|
|1.5.4|2020年03月31日|-   支持集群流控特性。
-   支持SAE方式接入。 |
|1.5.3|2020年03月9日|-   添加SOFARPC埋点支持。
-   埋点资源名增加长度限制（最长1024字符）。
-   MyBatis adapter新增DAO mapper方法埋点支持。
-   日志依赖优化。 |
|1.5.2|2020年02月19日|-   去除RT统计限制。
-   去除多余日志依赖。 |
|1.5.1|2019年12月27日|-   修复控制台应用名和实际监听规则对应的appName不同步的问题。
-   MyBatis适配改进SQL含换行符情况下的处理，避免影响监控日志格式。 |
|1.5.0|2019年11月27日|-   同步基线至Sentinel开源1.7.0版本。
-   增加通用配置功能，支持动态配置。
-   增加热点规则支持。
-   优化内存占用情况。 |
|1.4.5|2019年10月23日|-   适配低版本的MyBatis，修复不兼容低版本MyBatis的问题。
-   支持通过参数的方式自定义Web默认限流页面的HTTP状态码。 |
|1.4.3|无|-   系统规则maxCpuUsage模式策略调整，不再进行BBR判断。
-   修复依赖冲突问题。 |
|1.4.2|无|修复PropertyUrlCleaner自动注册判断逻辑的问题。|
|1.4.1|无|-   优化系统指标信息采集方式，拉取监控的时候系统指标信息通过Dubbo Metrics采集。
-   引入MyBatis adapter支持。

**说明：** 此版本开始不支持和开源依赖混用。 |
|1.4.0|无|-   同步基线至Sentinel开源1.6.3版本。
-   支持文件配置URL埋点清理。 |
|1.3.6|无|同步基线至Sentinel开源1.6.2版本。|
|1.3.5|无|-   同步基线至Sentinel开源1.6.1版本。
-   监控指标支持CPU使用率和load。 |

**Spring-Boot-Starter-AHAS-Sentinel-Client版本说明**

|版本|发布时间|版本说明|
|--|----|----|
|1.8.9|2021年04月09日|特性对应ahas-sentinel-client 1.8.9。|
|1.8.8|2021年04月02日|新增Spring RestTemplate适配。|
|1.8.7|2021年03月12日|-   完善Spring Cloud动态配置场景下解析AppName的逻辑。
-   特性对应ahas-sentinel-client 1.8.7。 |
|1.8.6|2021年02月05日|特性对应ahas-sentinel-client 1.8.6。|
|1.8.5|2021年02月01日|特性对应ahas-sentinel-client 1.8.5。|
|1.8.4|2021年01月28日|添加Feign埋点支持（支持Spring Cloud F/G/H三大版本体系）。|
|1.8.3|2021年01月13日|特性对应ahas-sentinel-client 1.8.3。|
|1.8.2|2021年01月09日|完善starter在application.properties动态配置场景下解析、更新配置的逻辑。|
|1.8.1|2020年12月23日|完善starter配置解析逻辑以解决部分场景下启动顺序导致配置读不到的问题。|
|1.8.0|2020年12月16日|特性对应ahas-sentinel-client 1.8.0。|
|1.7.5|2020年12月08日|特性对应ahas-sentinel-client 1.7.5。|
|1.7.3|2020年11月03日|特性对应ahas-sentinel-client 1.7.3。|
|1.7.2|2020年10月20日|特性对应ahas-sentinel-client 1.7.2。|
|1.7.1|2020年09月28日|特性对应ahas-sentinel-client 1.7.1。|
|1.6.6|2020年08月28日|特性对应ahas-sentinel-client 1.6.6。|
|1.6.5|2020年08月07日|特性对应ahas-sentinel-client 1.6.5。|
|1.6.4|2020年07月17日|特性对应ahas-sentinel-client 1.6.4。|
|1.6.3|2020年06月12日|特性对应ahas-sentinel-client 1.6.3。|
|1.6.2|2020年05月28日|特性对应ahas-sentinel-client 1.6.2。|
|1.6.1|2020年04月29日|特性对应ahas-sentinel-client 1.6.1。|
|1.6.0|2020年04月24日|特性对应ahas-sentinel-client 1.6.0。|
|1.5.5|2020年04月14日|特性对应ahas-sentinel-client 1.5.5。|
|1.5.4|2020年03月31日|特性对应ahas-sentinel-client 1.5.4。|
|1.5.3|2020年03月09日|-   特性对应AHAS-Sentinel-Client 1.5.3。
-   Spring Web Interceptor埋点资源名支持添加HTTP Mmethod前缀。
-   MyBatis默认埋点改为DAO Mapper埋点，可通过开关控制。 |
|1.5.2|2020年02月19日|特性对应AHAS-Sentinel-Client 1.5.2。|
|1.5.1|2019年12月27日|-   特性对应AHAS-Sentinel-Client 1.5.1。
-   该版本开始引入后会自动注册Spring Web interceptor（仅针对Web Servlet应用）、注解aspect、MyBatis interceptor（仅针对用了MyBatis的应用）。

**说明：** 用户从旧版本升级至1.5.1+ 版本时，需要去除之前自行注册的CommonFilter、SpringWebInterceptor等bean。 |
|1.5.0|2019年11月27日|特性对应AHAS-Sentinel-Client 1.5.0。|
|1.3.6|无|特性对应AHAS-Sentinel-Client 1.4.2。**说明：** 此版本开始不支持和开源依赖混用。 |
|1.3.5|无|-   特性对应AHAS-Sentinel-Client 1.4.0。
-   增加Spring Web Interceptor支持 \(REST API pattern自动提取）。 |

**Spring-Cloud-Gateway-Starter-AHAS-Sentinel版本说明**

|版本号|版本说明|
|---|----|
|1.3.6|-   完善Spring Cloud动态配置场景下解析AppName的逻辑。
-   特性对应Spring-Boot-Starter-AHAS-Sentinel-Client 1.8.7版本。 |
|1.3.5|特性对应Spring-Boot-Starter-AHAS-Sentinel-Client 1.8.6版本。|
|1.3.4|特性对应Spring-Boot-Starter-AHAS-Sentinel-Client 1.8.5版本。|
|1.3.3|特性对应Spring-Boot-Starter-AHAS-Sentinel-Client 1.8.4版本，主动降级规则支持在控制台配置自定义fallback行为。|
|1.3.2|特性对应Spring-Boot-Starter-AHAS-Sentinel-Client 1.8.3版本。|
|1.3.1|特性对应Spring-Boot-Starter-AHAS-Sentinel-Client 1.8.2版本。|
|1.3.0|特性对应Spring-Boot-Starter-AHAS-Sentinel-Client 1.8.1版本。|
|1.2.4|特性对应Spring-Boot-Starter-AHAS-Sentinel-Client 1.8.0版本。|
|1.2.3|特性对应Spring-Boot-Starter-AHAS-Sentinel-Client 1.7.5版本。|
|1.2.2|特性对应Spring-Boot-Starter-AHAS-Sentinel-Client 1.7.3版本。|
|1.2.1|特性对应Spring-Boot-Starter-AHAS-Sentinel-Client 1.7.1版本。|
|1.1.7|特性对应Spring-Boot-Starter-AHAS-Sentinel-Client 1.6.3版本。|
|1.1.6|特性对应Spring-Boot-Starter-AHAS-Sentinel-Client 1.6.1版本。|
|1.1.5|特性对应Spring-Boot-Starter-AHAS-Sentinel-Client 1.6.0版本。|
|1.1.4|特性对应Spring-Boot-Starter-AHAS-Sentinel-Client 1.5.3版本。|
|1.1.3|特性对应Spring-Boot-Starter-AHAS-Sentinel-Client 1.5.2版本。|
|1.1.2|修复某些特殊情况下getServletPath为空导致API匹配不成功的问题。|
|1.1.1|特性对应Spring-Boot-Starter-AHAS-Sentinel-Client 1.5.1版本。|
|1.1.0|特性对应Spring-Boot-Starter-AHAS-Sentinel-Client 1.5.0版本。**说明：** 此版本开始不支持和开源依赖混用。 |

**Spring-Cloud-Zuul-Starter-AHAS-Sentinel版本说明**

|版本号|版本说明|
|---|----|
|1.3.6|-   完善Spring Cloud动态配置场景下解析AppName的逻辑。
-   特性对应Spring-Boot-Starter-AHAS-Sentinel-Client 1.8.7版本。 |
|1.3.5|特性对应Spring-Boot-Starter-AHAS-Sentinel-Client 1.8.6版本。|
|1.3.4|特性对应Spring-Boot-Starter-AHAS-Sentinel-Client 1.8.5版本。|
|1.3.3|特性对应Spring-Boot-Starter-AHAS-Sentinel-Client 1.8.4版本。|
|1.3.2|特性对应Spring-Boot-Starter-AHAS-Sentinel-Client 1.8.3版本。|
|1.3.1|特性对应Spring-Boot-Starter-AHAS-Sentinel-Client 1.8.2版本。|
|1.3.0|特性对应Spring-Boot-Starter-AHAS-Sentinel-Client 1.8.1版本。|
|1.2.4|特性对应Spring-Boot-Starter-AHAS-Sentinel-Client 1.8.0版本。|
|1.2.3|支持与AHAS Sentinel Java Agent同时使用，SDK在探测到Agent相关类存在时不会触发初始化，网关适配模块不会重复生效。|
|1.2.2|特性对应Spring-Boot-Starter-AHAS-Sentinel-Client 1.7.3版本。|
|1.2.1|特性对应Spring-Boot-Starter-AHAS-Sentinel-Client 1.7.1版本。|
|1.1.7|特性对应Spring-Boot-Starter-AHAS-Sentinel-Client 1.6.3版本。|
|1.1.6|特性对应Spring-Boot-Starter-AHAS-Sentinel-Client 1.6.1版本。|
|1.1.5|特性对应Spring-Boot-Starter-AHAS-Sentinel-Client 1.6.0版本。|
|1.1.4|特性对应Spring-Boot-Starter-AHAS-Sentinel-Client 1.5.3版本。|
|1.1.3|特性对应Spring-Boot-Starter-AHAS-Sentinel-Client 1.5.2版本。|
|1.1.2|修复某些特殊情况下getServletPath为空导致API匹配不成功的问题。|
|1.1.1|特性对应Spring-Boot-Starter-AHAS-Sentinel-Client 1.5.1版本。|
|1.1.0|特性对应Spring-Boot-Starter-AHAS-Sentinel-Client 1.5.0版本。**说明：** 此版本开始不支持和开源依赖混用。 |

## Java Agent

|版本号|版本说明|
|---|----|
|1.8.0|-   新增Spring Web插件支持（REST API会自动提取pattern），原有的Servlet插件默认不开启。
-   新增MyBatis插件支持，原有的JDBC插件默认不开启。
-   同步SDK 1.7.x最新相关特性（自适应流控）。 |
|1.7.10|-   修复熔断降级模块在同资源配置多个规则时可能出现无法从half-open状态中恢复的问题。
-   修复fastjson版本导致JDK 1.7下Agent无法正常工作的问题。 |
|1.7.9|-   集群流控支持单机大流量场景（批量请求）。
-   修复熔断降级规则阈值比例为100%时不生效的问题。 |
|1.7.8|-   修复Spring Cloud Gateway、Zuul等网关插件不生效的问题。
-   应用appType支持通过环境变量配置。 |
|1.7.7|修复JDK 11下agent初始化失败的问题。|
|1.7.6|熔断降级支持渐进式恢复策略。|
|1.7.5|-   熔断降级特性改进：引入半开启探测模式，支持任意统计时长，RT模式改进为慢调用比例模式。
-   集群流控通信与异常处理优化。
-   支持张家口region。 |
|1.7.4|-   支持集群流控特性。
-   支持SAE方式接入。 |
|1.7.3|支持MySQL CJ Driver的SQL埋点。|
|1.7.2|-   支持启动参数和环境变量控制所有插件模块的开启和关闭。
-   改进SQL含换行符情况下的处理，添加SQL埋点长度限制。
-   去除RT统计限制。
-   修复部分非daemon线程导致main函数执行结束后无法退出的问题。 |
|1.7.1|-   同步基线至开源1.7.0版本，优化内存占用。
-   增加通用配置功能，支持簇点数目限制、context数目限制、来源数目限制、最大统计RT等基础配置项，支持动态配置。
-   增加热点规则支持。
-   默认关闭MQ相关插件以提升启动速度。 |
|1.7.0|新增Memcached \(spymemcached\)、gRPC、Jedis、RocketMQ（callback模式）、RabbitMQ插件支持。**说明：** MQ插件可能会导致应用启动速度变慢。 |
|1.6.0|新增MySQL（5.x driver）或Oracle SQL埋点支持。|

