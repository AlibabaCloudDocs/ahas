---
keyword: [Go应用, SDK接入, 应用防护]
---

# 接入Go应用

将Go应用接入AHAS应用防护后，可以对其配置流控、隔离和系统规则来保证系统稳定性。本文介绍如何使用SDK方式将Go应用接入应用防护。

确保Go应用的版本为1.13.0或以上，并通过Go Modules管理依赖。

## Dubbo、Gin Web、gRPC应用接入步骤

1.  登录[AHAS控制台](https://ahas.console.aliyun.com)，然后在页面左上角选择**地域**。

2.  在控制台左侧导航栏中选择**流量防护** \> **应用防护**。

3.  在应用防护页面右上角单击**新应用接入**，然后在**GO语言**页签下，选择**SDK接入**。

4.  单击**下载AHAS Go SDK**，然后将安装包解压到本地。

5.  打开您的Go工程，并在go.mod文件中添加以下依赖。

    **说明：**

    -   /path/to/aliyun-ahas-go-sdk是示例路径，请替换为Go SDK的解压路径。
    -   请确保您的Go版本≥1.13.0，并开启Go modules支持。
    ```
    require github.com/aliyun/aliyun-ahas-go-sdk v1.0.0
    #将后面的路径替换为AHAS Go SDK解压后的本地路径。
    replace github.com/aliyun/aliyun-ahas-go-sdk => /path/to/aliyun-ahas-go-sdk
    ```

6.  添加AHAS Sentinel初始化命令，并在应用启动时生效。

    ```
    import (
        ahas "github.com/aliyun/aliyun-ahas-go-sdk"
    )
    
    // 在应用的初始化逻辑中加入以下代码。
    // Sentinel core的初始化包含在了这里面。如果之前有调用过Sentinel的初始化函数，需要去掉。
    err := ahas.InitAhasDefault()
    if err != nil {
        log.Fatalf("Failed to init AHAS: %+v", err)
    }
    ```

7.  使用以下代码包住您的业务逻辑。示例代码如下。

    **说明：**

    -   Dubbo应用是在代码中通过import包的形式引入Dubbo adapter，其中的init\(\)函数会自动注入相关filter。Dubbo-Go版本需要≥1.3.0。Sentinel Dubbo adapter会自动统计所有provider和consumer的调用。
    -   Gin Web应用在Gin的初始化代码中引入SentinelMiddleware。Sentinel会对每个API route进行统计，资源名称类似于GET:/foo/:id。默认的限流处理逻辑是返回`429 (Too Many Requests)`错误码。
    -   gRPC应用在gRPC的初始化代码中引入Sentinel提供的interceptor，Sentinel针对Server和Client都提供了unary和streaming两种interceptor，以上代码以Server端为例。默认的限流处理逻辑是返回Sentinel的BlockError。您也可以在创建interceptor时提供自定义的fallback处理逻辑。
    -   在Go-Micro的初始化代码中引入Sentinel提供的wrapper。Sentinel针对Go-Micro Server和Client都提供了wrapper。以上代码以Server端为例。埋点默认会提取服务method作为资源名，默认的流控处理逻辑是返回Sentinel的BlockError。您也可以在创建wrapper时提供自定义的fallback处理逻辑。
8.  配置AHAS，在项目目录下新建sentinel.yml文件，配置文件内容如下。

    若在公网地域，需要查看License信息。请在**GO语言**页签查看（非公网地域不需要），具体请参见[查看License](/cn.zh-CN/流量防护/应用防护/参考信息/查看License.md)。

    ![Go license](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/0733858951/p139654.png)

9.  重启您的应用。


## 自定义埋点接入步骤

通过自定义埋点接入Go语言的步骤如下。

1.  登录[AHAS控制台](https://ahas.console.aliyun.com)，然后在页面左上角选择**地域**。

2.  在控制台左侧导航栏中选择**流量防护** \> **应用防护**。

3.  在应用防护页面右上角单击**新应用接入**，然后在**GO语言**页签下，选择**SDK接入**。

4.  单击**下载AHAS Go SDK**，然后将安装包解压到本地。

5.  打开您的Go工程，并在go.mod文件中添加以下依赖。

    **说明：** /path/to/aliyun-ahas-go-sdk是示例路径，请替换为Go SDK的解压路径。

    ```
    require github.com/aliyun/aliyun-ahas-go-sdk v1.0.0
    replace github.com/aliyun/aliyun-ahas-go-sdk => /path/to/aliyun-ahas-go-sdk
    ```

6.  添加import依赖。

    ```
    import (
      ahas "github.com/aliyun/aliyun-ahas-go-sdk"
      sentinel "github.com/alibaba/sentinel-golang/api"
    )
    ```

7.  添加AHAS Sentinel初始化命令，并在应用启动时生效。

    ```
    // 在应用的初始化逻辑中加入以下代码
    // Sentinel core的初始化包含在了这里面。如果之前有调用过Sentinel的初始化函数，需要去掉。
    
    err:= ahas.InitAhasDefault()
    if err!= nil{
      log.Fatalf("Failed to init AHAS:%+v", err)
    }
    ```

8.  使用以下代码包住您的业务逻辑，埋点方法及示例请参见[Sentinel Go API](#section_obl_5t6_zpy)。

    ```
    import (
        sentinel "github.com/alibaba/sentinel-golang/api"
    )
    
    // Entry方法用于埋点。
    e, b := sentinel.Entry("your-resource-name", sentinel.WithTrafficType(base.Inbound))
    if b != nil {
        // 请求被流控，可以从BlockError中获取限流详情。
    } else {
        // 请求可以通过，在此处编写您的业务逻辑。
        // 务必保证业务逻辑结束后Exit。
        e.Exit()
    }
    ```

9.  使用以下任意一种方式配置AHAS Sentinel。

    -   YAML文件配置。

        AHAS支持的YAML配置项如下：

        **说明：**

        -   若通过InitAhasFromFile\(path\)初始化AHAS，则会从path指定的YAML文件中读取配置项。
        -   若通过InitAhasDefault\(\)初始化AHAS，则会尝试从SENTINEL\_CONFIG\_FILE\_PATH环境变量读取path并读取对应的文件。若未指定则默认从项目目录下的sentinel.yml文件读取配置。
        -   若均不存在，AHAS则会通过环境变量读取基础的配置（如项目名称），其他配置项采用默认值。注意环境变量配置会覆盖配置文件的配置。
        |Key|对应的YAML配置项|含义|备注|
        |---|----------|--|--|
        |`SENTINEL_APP_NAME`|sentinel.app.name|项目名称|必需的配置项，若不配置则标为`unknown_go_service`。|
        |`SENTINEL_CONFIG_FILE_PATH`|无|YAML配置文件路径|若未指定则默认从项目目录下的`sentinel.yml`文件读取配置。|
        |`AHAS_LICENSE`|ahas.license|AHAS License|公网环境必需，Region环境不需要。|
        |`AHAS_NAMESPACE`|ahas.namespace|AHAS命名空间|默认为Default。需在控制台预先添加后配置，不可随便指定。|
        |`SENTINEL_LOG_DIR`|无|日志路径|默认路径为`~/logs/csp`。|
        |`SENTINEL_LOG_USE_PID`|无|日志文件是否带Pid|默认为False。|

        配置文件示例：

    -   配置环境变量。

## Sentinel Go API

使用Sentinel的Entry API将业务逻辑封装起来，这一步称为**埋点**。每个埋点都有一个资源名称（resource），代表触发了这个资源的调用或访问。

埋点API位于API包中，一般为`Entry(resource string, opts ...Option) (*base.SentinelEntry, *base.BlockError)`，其中resource代表埋点资源名，opts代表埋点配置。目前支持以下埋点配置：

-   WithTrafficType\(entryType base.TrafficType\)：标记该埋点资源的流量类型，其中Inbound代表入口流量，Outbound代表出口流量。若不指定，默认为Outbound。
-   WithResourceType\(resourceType base.ResourceType\)：标记该埋点资源的分类。
-   WithAcquireCount\(acquireCount uint32\)：标记每次触发该埋点计为几次调用（可以理解为batch count）。若不指定，默认为1。
-   WithArgs\(args ...interface\{\}\)：埋点携带的参数列表，为热点参数统计预留。

埋点API示例。

```
import (
    sentinel "github.com/alibaba/sentinel-golang/api"
)

// Entry方法用于埋点。
e, b := sentinel.Entry("your-resource-name", sentinel.WithTrafficType(base.Inbound))
if b != nil {
    // 请求被流控，可以从BlockError中获取限流详情。
} else {
    // 请求可以通过，在此处编写您的业务逻辑。
    // 务必保证业务逻辑结束后Exit。
e.Exit()
}
```

**说明：** 若该次调用被拒绝，则Entry API会返回BlockError代表被Sentinel限流。BlockError提供了限流原因以及触发的规则等信息，可以方便开发者获取相关信息进行记录和处理。

## 结果验证

登录[AHAS控制台](https://ahas.console.aliyun.com)，在左侧导航栏选择**流量防护** \> **应用防护**，若在应用防护页面出现该应用的资源卡片且有数据上报，则说明接入成功。

![应用防护.png](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/1733858951/p139423.png)

## 相关操作

给Go SDK应用配置规则，目前支持流控规则（暂不支持集群流控）、隔离规则、降级规则、系统规则和热点规则。

-   [配置流控规则](/cn.zh-CN/流量防护/应用防护/配置规则/配置流控规则.md)
-   [配置隔离规则](/cn.zh-CN/流量防护/应用防护/配置规则/配置隔离规则.md)
-   [配置熔断规则](/cn.zh-CN/流量防护/应用防护/配置规则/配置熔断规则.md)
-   [自适应流控](/cn.zh-CN/流量防护/应用防护/配置规则/自适应流控.md)
-   [配置热点规则](/cn.zh-CN/流量防护/应用防护/配置规则/配置热点规则.md)

