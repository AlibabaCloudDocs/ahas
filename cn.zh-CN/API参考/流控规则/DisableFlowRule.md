# DisableFlowRule

调用DisableFlowRule接口关闭流控规则。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=ahas-openapi&api=DisableFlowRule&type=RPC&version=2019-09-01)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|DisableFlowRule|系统规定参数。取值：DisableFlowRule。 |
|RuleId|Long|是|123|流控规则ID。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|Code|String|200|返回码。 |
|Data|Struct| |流控规则数据。 |
|AppName|String|ahas-demo|应用名，若为EDAS应用，则AppName为EDAS中的App ID，可在EDAS控制台“应用管理\>基本信息”中查看对应的ID。 |
|ClusterEstimatedMaxQps|Float|5000|集群接口预估最大QPS。 |
|ClusterFallbackStrategy|Integer|0|集群流控通信失败退化策略，0表示退化到单机，1表示直接通过。 |
|ClusterFallbackThreshold|Integer|30|退化单机阈值，当退化策略为退化到单机（ClusterFallbackStrategy=0）时返回。 |
|ClusterMode|Boolean|true|是否为集群模式。 |
|ClusterThresholdType|Integer|0|阈值模式，0表示单机均摊阈值，1表示集群阈值。 |
|ControlBehavior|Integer|0|流控效果。0表示快速失败，1表示预热启动，2表示排队等待。 |
|Enable|Boolean|false|是否开启。 |
|LimitOrigin|String|default|来源应用。 |
|MaxQueueingTimeMs|Integer|2000|超时时间。 |
|Namespace|String|default|命名空间。 |
|RefResource|String|handleServiceB|关联接口名、入口资源名。 |
|RelationStrategy|Integer|0|统计维度。 |
|Resource|String|handleServiceA|资源名。 |
|RuleId|Long|123|流控规则ID。 |
|StatDurationMs|Integer|5000|集群模式下统计窗口时长。 |
|Threshold|Float|300|阈值。 |
|WarmUpPeriodSec|Integer|30|预热时间。 |
|Message|String|null|错误信息。 |
|RequestId|String|3FEEAD12-CE22-4EDE-A729-CE94EC070610|请求ID。 |
|Success|Boolean|true|是否成功。 |

## 示例

请求示例

```
http(s)://[Endpoint]/?Action=DisableFlowRule
&RuleId=123
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<DisableFlowRuleResponse>
  <Message>null</Message>
  <RequestId>3FEEAD12-CE22-4EDE-A729-CE94EC070610</RequestId>
  <Data>
        <RefResource>handleServiceB</RefResource>
        <ClusterMode>true</ClusterMode>
        <RuleId>123</RuleId>
        <Resource>handleServiceA</Resource>
        <MaxQueueingTimeMs>2000</MaxQueueingTimeMs>
        <Namespace>default</Namespace>
        <AppName>ahas-demo</AppName>
        <WarmUpPeriodSec>30</WarmUpPeriodSec>
        <ClusterThresholdType>0</ClusterThresholdType>
        <ClusterFallbackStrategy>0</ClusterFallbackStrategy>
        <ControlBehavior>0</ControlBehavior>
        <ClusterFallbackThreshold>30</ClusterFallbackThreshold>
        <Enable>false</Enable>
        <RelationStrategy>0</RelationStrategy>
        <LimitOrigin>default</LimitOrigin>
        <ClusterEstimatedMaxQps>5000</ClusterEstimatedMaxQps>
        <Threshold>300</Threshold>
        <StatDurationMs>5000</StatDurationMs>
  </Data>
  <Code>200</Code>
  <Success>true</Success>
</DisableFlowRuleResponse>
```

`JSON` 格式

```
{
    "Message":"null",
    "RequestId":"3FEEAD12-CE22-4EDE-A729-CE94EC070610",
    "Data":
    {
        "RefResource":"handleServiceB",
        "ClusterMode":"true",
        "RuleId":"123",
        "Resource":"handleServiceA",
        "MaxQueueingTimeMs":"2000",
        "Namespace":"default",
        "AppName":"ahas-demo",
        "WarmUpPeriodSec":"30",
        "ClusterThresholdType":"0",
        "ClusterFallbackStrategy":"0",
        "ControlBehavior":"0",
        "ClusterFallbackThreshold":"30",
        "Enable":"false",
        "RelationStrategy":"0",
        "LimitOrigin":"default",
        "ClusterEstimatedMaxQps":"5000",
        "Threshold":"300",
        "StatDurationMs":"5000"
    },
    "Code":"200",
    "Success":"true"
}
```

## 错误码

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|400|IllegalArgument.RuleId|The specified RuleId is invalid.|参数RuleId不合法|

访问[错误中心](https://error-center.aliyun.com/status/product/ahas-openapi)查看更多错误码。

