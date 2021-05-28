# CreateFlowRule

调用CreateFlowRule接口创建流控规则。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=ahas-openapi&api=CreateFlowRule&type=RPC&version=2019-09-01)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|CreateFlowRule|系统规定参数。取值：**CreateFlowRule**。 |
|Namespace|String|是|default|命名空间。 |
|AppName|String|是|ahas-demo|应用名，若为EDAS应用，则AppName为EDAS中的App ID，可在EDAS控制台“应用管理\>基本信息”中查看对应的ID。 |
|RelationStrategy|Integer|是|0|统计维度。0表示当前接口，1表示关联接口，2表示链路入口。 |
|Threshold|Float|是|50|阈值。 |
|Enable|Boolean|否|true|规则是否开启，默认为false。 |
|Resource|String|是|handleServiceA|资源名。 |
|LimitOrigin|String|否|default|来源应用，默认为default。 |
|RefResource|String|否|handleServiceB|关联接口名、入口资源名。当统计维度relationStrategy值为1（关联接口）或2（链路入口）时，需要设置该字段。 |
|ControlBehavior|Integer|是|0|流控效果。0表示快速失败，1表示预热启动，2表示排队等待。 |
|WarmUpPeriodSec|Integer|否|30|预热时间。当controlBehavior值为1（预热启动）时，需要设置该字段。 |
|MaxQueueingTimeMs|Integer|否|2000|超时时间。当controlBehavior值为2（排队等待）时，需要设置该字段。 |
|AhasRegionId|String|否|cn-hangzhou|地域 |

详细参数解释，请参见[配置流控规则](~~101077~~)。

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|Message|String|null|错误信息。 |
|RequestId|String|3FEEAD12-CE22-4EDE-A729-CE94EC070610|请求ID。 |
|Data|Object| |返回数据。 |
|RefResource|String|handleServiceB|关联接口名、入口资源名。 |
|ClusterFallbackThreshold|Integer|30|退化单机阈值，当退化策略为退化到单机（ClusterFallbackStrategy=0）时返回。 |
|Namespace|String|default|命名空间。 |
|LimitOrigin|String|default|来源应用。 |
|StatDurationMs|Integer|5000|集群模式下统计窗口时长。 |
|ClusterThresholdType|Integer|0|阈值模式，0表示单机均摊阈值，1表示集群阈值。 |
|RuleId|Long|123|规则ID。 |
|RelationStrategy|Integer|0|统计维度。 |
|AppName|String|ahas-demo|应用名，若为EDAS应用，则AppName为EDAS中的App ID，可在EDAS控制台“应用管理\>基本信息”中查看对应的ID。 |
|Resource|String|handleServiceA|资源名。 |
|ClusterEstimatedMaxQps|Float|5000|集群接口预估最大QPS。 |
|ControlBehavior|Integer|0|流控效果。0表示快速失败，1表示预热启动，2表示排队等待。 |
|MaxQueueingTimeMs|Integer|2000|超时时间。 |
|ClusterFallbackStrategy|Integer|0|集群流控通信失败退化策略，0表示退化到单机，1表示直接通过。 |
|WarmUpPeriodSec|Integer|30|预热时间。 |
|ClusterMode|Boolean|true|是否为集群模式。 |
|Threshold|Float|300|阈值。 |
|Enable|Boolean|true|规则是否开启。 |
|Code|String|200|返回码。返回200代表成功。 |
|Success|Boolean|true|是否成功。 |

## 示例

请求示例

```
http(s)://[Endpoint]/?Action=CreateFlowRule
&AppName=ahas-demo
&ControlBehavior=0
&Namespace=default
&RelationStrategy=0
&Resource=handleServiceA
&Threshold=50
&<公共请求参数>
```

正常返回示例

`XML`格式

```
HTTP/1.1 200 OK
Content-Type:application/xml

<CreateFlowRuleResponse>
    <Message>null</Message>
    <RequestId>3FEEAD12-CE22-4EDE-A729-CE94EC070610</RequestId>
    <Data>
        <RefResource>handleServiceB</RefResource>
        <ClusterFallbackThreshold>30</ClusterFallbackThreshold>
        <Namespace>default</Namespace>
        <LimitOrigin>default</LimitOrigin>
        <StatDurationMs>5000</StatDurationMs>
        <ClusterThresholdType>0</ClusterThresholdType>
        <RuleId>123</RuleId>
        <RelationStrategy>0</RelationStrategy>
        <AppName>ahas-demo</AppName>
        <Resource>handleServiceA</Resource>
        <ClusterEstimatedMaxQps>5000</ClusterEstimatedMaxQps>
        <ControlBehavior>0</ControlBehavior>
        <MaxQueueingTimeMs>2000</MaxQueueingTimeMs>
        <ClusterFallbackStrategy>0</ClusterFallbackStrategy>
        <WarmUpPeriodSec>30</WarmUpPeriodSec>
        <ClusterMode>true</ClusterMode>
        <Threshold>300</Threshold>
        <Enable>true</Enable>
    </Data>
    <Code>200</Code>
    <Success>true</Success>
</CreateFlowRuleResponse>
```

`JSON`格式

```
HTTP/1.1 200 OK
Content-Type:application/json

{
  "Message" : "null",
  "RequestId" : "3FEEAD12-CE22-4EDE-A729-CE94EC070610",
  "Data" : {
    "RefResource" : "handleServiceB",
    "ClusterFallbackThreshold" : 30,
    "Namespace" : "default",
    "LimitOrigin" : "default",
    "StatDurationMs" : 5000,
    "ClusterThresholdType" : 0,
    "RuleId" : 123,
    "RelationStrategy" : 0,
    "AppName" : "ahas-demo",
    "Resource" : "handleServiceA",
    "ClusterEstimatedMaxQps" : 5000,
    "ControlBehavior" : 0,
    "MaxQueueingTimeMs" : 2000,
    "ClusterFallbackStrategy" : 0,
    "WarmUpPeriodSec" : 30,
    "ClusterMode" : true,
    "Threshold" : 300,
    "Enable" : true
  },
  "Code" : "200",
  "Success" : true
}
```

## 错误码

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|400|IllegalArgument.AppName|The specified AppName is invalid.|参数AppName不合法|
|400|IllegalArgument.MaxQueueingTimeM|The specified MaxQueueingTimeMs is invalid.|参数MaxQueueingTimeMs不合法|
|400|IllegalArgument.Namespace|The specified Namespace is invalid.|参数Namespace不合法|
|400|IllegalArgument.RefResource|The specified RefResource is invalid.|参数RefResource不合法|
|400|IllegalArgument.RelationStrategy|The specified RelationStrategy is invalid.|参数RelationStrategy不合法|
|400|IllegalArgument.Resource|The specified Resource is invalid.|参数Resource不合法|
|400|IllegalArgument.Threshold|The specified Threshold is invalid.|参数Threshold不合法|
|400|IllegalArgument.WarmUpPeriodSec|The specified WarmUpPeriodSec is invalid.|参数WarmUpPeriodSec不合法|

访问[错误中心](https://error-center.aliyun.com/status/product/ahas-openapi)查看更多错误码。

