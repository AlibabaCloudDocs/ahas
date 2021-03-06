---
keyword: [服务压测, 限流, Dubbo]
---

# 压测Dubbo服务

应用压测功能通过对系统的压测，得到一系列的性能指标，从而指导您配置最优的防护规则，实现业务的高可用。本文介绍压测Dubbo服务的操作步骤。

应用已接入AHAS应用防护，具体操作，请参见[接入应用方式](/cn.zh-CN/流量防护/应用防护/接入应用/接入应用方式.md)。

应用压测需要满足以下条件才有功能入口：

-   应用SDK版本是1.8.5及以上。
-   应用防护为高级防护模式。
-   非公网环境。

## 步骤一：创建压测场景

1.  登录[AHAS控制台](https://ahas.console.aliyun.com)，然后在页面左上角选择**地域**。

2.  在控制台左侧导航栏中选择**流量防护** \> **应用防护**。

3.  在应用防护页面单击目标应用卡片。

4.  在应用详情页的左侧导航栏选择**接口详情**，然后单击**RPC服务**页签。

5.  在接口详情页面，单击![创建场景.png](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/2640622161/p238049.png)图标。

6.  在**压测配置**面板中设置**场景配置**和**压力配置**相关参数。

    **场景配置**页签相关参数说明如下。

    |参数|描述|示例|
    |--|--|--|
    |**场景名称**|压测场景名称。|test-dubbo|
    |**服务地址**|包括IP和端口。您可以根据应用实际端口进行配置，多个服务地址以英文逗号（,）分隔。|    -   192.168.xx.xx:20880
    -   192.168.xx.xx,192.168.xx.xx:20880 |
    |**应用**|输入需要压测的应用。|Demo-service|
    |**组别**（可选）|Dubbo微服务组别group。|local|
    |**版本**（可选）|Dubbo微服务版本version。|1.0|
    |**服务**|输入应用的服务。|com.alibaba.csp.demo.OrderService|
    |**方法**|输入服务的方法。关于Dubbo服务的方法参数类型及配置方式，请参见[Dubbo参考示例](#section_tid_ehh_jea)。|String sayHello\(String name\);|
    |**方法参数类型**|需要压测服务的函数包含的参数类型。填写的内容是一个字符串类型的JSON数组，数组的每一位代表对应位置的参数类型。除了Java基本类型，其余类型需要填写完整的类路径。关于Dubbo服务的方法参数类型及配置方式，请参见[Dubbo参考示例](#section_tid_ehh_jea)。|\["java.lang.String"\]|
    |**请求参数**|设置请求参数。关于Dubbo服务的方法参数类型及配置方式，请参见[Dubbo参考示例](#section_tid_ehh_jea)。|\["hello, dubbo"\]|
    |**超时时间（毫秒）**|设置超时时间，单位：毫秒。|1000|
    |**打印日志**|开启可自动打印日志信息，但会影响到服务压测性能，建议正常压测时关闭。|关闭|

    **压力配置**页签相关参数说明如下。

    |参数|描述|
    |--|--|
    |**压测模式**|TPS吞吐量模式（Transaction Per Second），指系统每秒处理的事务数量。|
    |**流量模型**|流量模型包括固定压力、阶梯压力和脉冲压力。    -   **固定压力**：以配置的固定并发值TPS进行施压。公测期间最大TPS为1000。
    -   **阶梯压力**：设置最大值、最小值、递增时长等信息。从最小值开始按照阶梯逐步递增，达到最大值后按照最大值持续施压。
    -   **脉冲压力**：设置峰值、谷值以及持续时间等信息，施压流量以峰值、峰谷的锯齿波的形式进行施压。 |
    |**TPS**|设置TPS，上限为1000。|
    |**压测时长（分钟）**|指压测总时长，公测期间压测时长3~10分钟。|


## 步骤二：执行压测任务

压测场景创建成功后，可以执行压测任务。

1.  在压测配置面板，单击**保存配置并启动压测**。

    **说明：** 压测环境准备需要等待约1分钟。

2.  在性能概要和实时性能数据区域，可以实时查看压测的性能指标。

    ![性能数据2.png](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/2640622161/p238078.png)


## 步骤三：查看压测报告

压测完成后，可以查看压测报告。

1.  在应用详情页的左侧导航栏选择**应用压测**，单击目标场景**操作**列的**详情**。

2.  在性能数据面板，查看压测报告。

    ![性能数据.png](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/2777250161/p214207.png)

    **说明：** **实时性能数据**统计的是每10秒的所有施压机数据，具体根据压测总时间长度会有所变化。单击图上方的图例，可以显示或隐藏某些数据曲线。

    |参数|说明|
    |--|--|
    |**总请求数**|整个压测过程中，共发起的请求个数。|
    |**平均TPS**|压测周期内，所有施压机发出的平均TPS值，TPS=调用总次数/总运行时间。|
    |**平均RT（ms）**|所有压力机发出平均响应时间。|
    |**最小RT（ms）**|所有压力机中最小的一次响应时间。|
    |**最大RT（ms）**|所有压力机中最大的一次响应时间。|
    |**错误请求数**|所有压力机中错误请求数之和。|
    |**错误率**|所有压力机中的平均错误率。|
    |**TP80（ms）**|所有压力机中80分位（P80）的平均值。|
    |**TP95（ms）**|所有压力机中95分位（P95）的平均值。|
    |**TP99（ms）**|所有压力机中99分位（P99）的平均值。|

3.  在性能数据面板，单击**下载日志**，可获取压测过程中的日志。


## 步骤四：设置防护规则

您可以根据压测报告的结果，在AHAS的应用防护中设置防护规则。在应用详情页的左侧导航栏，选择**规则管理**。具体操作，请参见[配置流控规则](/cn.zh-CN/流量防护/应用防护/配置规则/配置流控规则.md)。

## Dubbo参考示例

|方法|参数类型填写方式|参数填写方式|
|--|--------|------|
|String sayHello\(String name\);|\["java.lang.String"\]|\["hello, dubbo"\]|
|String helloBean\(HelloBean helloBean\);|\["com.alibaba.dubbo.api.DemoService"\]|\[\{"booleanValue":true,"helloSubValue":\{"booleanValue":false,"intValue":2,"stringValue":"subbean"\},"intValue":1,"stringValue":"bean"\}\]|
|String helloBean\(HelloBean helloBean1, HelloBean helloBean2\);|\["com.alibaba.dubbo.api.DemoService","com.alibaba.pts.dubbo.api.DemoService"\]|\[\{"booleanValue":true,"helloSubValue":\{"booleanValue":false,"intValue":2,"stringValue":"subbean"\},"intValue":1,"stringValue":"bean"\},\{"booleanValue":true,"helloSubValue":\{"booleanValue":false,"intValue":2,"stringValue":"subbean"\},"intValue":1,"stringValue":"bean"\}\]|
|String helloMap\(Map helloMap\);|\["java.util.Map"\]|\[\{"booleanValue":true,"helloSubValue":\{"booleanValue":false,"intValue":2,"stringValue":"subbean"\},"intValue":1,"stringValue":"bean"\}\]|
|String helloMap\(Map helloMap1, Map helloMap2\);|\["java.util.Map", "java.util.Map"\]|\[\{"booleanValue":true,"helloSubValue":\{"booleanValue":false,"intValue":2,"stringValue":"subbean"\},"intValue":1,"stringValue":"bean"\},\{"booleanValue":true,"helloSubValue":\{"booleanValue":false,"intValue":2,"stringValue":"subbean"\},"intValue":1,"stringValue":"bean"\}\]|
|String helloList\(List helloList\);|\["java.util.List"\]|\[\[1\]\]|
|String helloList\(List helloList1, List helloList2\);|\["java.util.List","java.util.List"\]|\[\[1\],\[1,2\]\]|
|String helloString\(String helloString\);|\["java.lang.String"\]|\[\[1\],\[1,2\],\[1,3\]\]|
|String helloString\(String helloString1, String helloString2\);|\["java.lang.String","java.lang.String"\]|\["hello, dubbo", "hello, dubbo"\]|
|String helloInt\(int helloInt\);|\["int"\]|\["hello, dubbo", "hello, dubbo"\]|
|String helloInt\(int helloInt1, int helloInt2\);|\["int","int"\]|\["1","2"\]|
|String helloBoolean\(boolean helloBoolean\);|\["boolean"\]|\["true"\]|
|String helloBoolean\(boolean helloBoolean1, boolean helloBoolean2\);|\["boolean","boolean"\]|\["true","false"\]|
|String helloVoid\(\);|\[\]|\[\]|

