# ModifyHotParamRule

调用ModifyHotParamRule接口修改热点规则。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=ahas-openapi&api=ModifyHotParamRule&type=RPC&version=2019-09-01)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|ModifyHotParamRule|系统规定参数。取值：**ModifyHotParamRule**。 |
|MetricType|Integer|否|1|统计维度，0表示并发数，1表示通过请求数。 |
|Threshold|Float|否|20|阈值。 |
|Enable|Boolean|否|false|规则是否开启。 |
|RuleId|Long|是|123|规则ID。 |
|ParamIdx|Integer|否|1|参数位置索引。 |
|StatDurationSec|Long|否|1|统计周期时间。 |
|ControlBehavior|Integer|否|0|流控效果，0表示快速失败，2表示排队等待。 |
|BurstCount|Integer|否|2|缓冲请求数，流控效果为快速失败时需要设置。 |
|MaxQueueingTimeMs|Integer|否|3000|超时时间，流控效果为排队等待时需要设置。 |
|AhasRegionId|String|否|cn-hangzhou|地域 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|Message|String|null|错误信息 |
|RequestId|String|3FEEAD12-CE22-4EDE-A729-CE94EC070610|请求ID |
|Data|Object| |返回数据 |
|ParamIdx|Integer|1|热点参数索引 |
|Namespace|String|default|命名空间 |
|ParamFlowItemList|Array of ParamFlowItemList| |热点参数例外项 |
|ItemValue|String|apple|例外项参数值 |
|ItemType|String|String|例外项类型 |
|Threshold|Float|20|例外项阈值 |
|StatDurationSec|Long|1|统计周期时间 |
|BurstCount|Integer|2|缓冲请求数 |
|RuleId|Long|123|热点规则ID |
|Resource|String|handleService|资源名 |
|AppName|String|ahas-demo|应用名，若为EDAS应用，则AppName为EDAS中的App ID，可在EDAS控制台“应用管理\>基本信息”中查看对应的ID。 |
|MaxQueueingTimeMs|Integer|3000|流控效果为排队等待时对应的超时时间。 |
|ControlBehavior|Integer|0|流控效果，0表示快速失败，2表示排队等待。 |
|MetricType|Integer|1|统计维度，0表示并发数，1表示通过请求数。 |
|Threshold|Float|20|单机阈值 |
|Enable|Boolean|false|规则是否开启 |
|Code|String|200|返回码 |
|Success|Boolean|true|是否成功 |

## 示例

请求示例

```
http(s)://[Endpoint]/?Action=ModifyHotParamRule
&RuleId=123
&<公共请求参数>
```

正常返回示例

`XML`格式

```
HTTP/1.1 200 OK
Content-Type:application/xml

<ModifyHotParamRuleResponse>
    <Message>null</Message>
    <RequestId>3FEEAD12-CE22-4EDE-A729-CE94EC070610</RequestId>
    <Data>
        <ParamIdx>1</ParamIdx>
        <Namespace>default</Namespace>
        <ParamFlowItemList>
            <ItemValue>apple</ItemValue>
            <ItemType>String</ItemType>
            <Threshold>20</Threshold>
        </ParamFlowItemList>
        <StatDurationSec>1</StatDurationSec>
        <BurstCount>2</BurstCount>
        <RuleId>123</RuleId>
        <Resource>handleService</Resource>
        <AppName>ahas-demo</AppName>
        <MaxQueueingTimeMs>3000</MaxQueueingTimeMs>
        <ControlBehavior>0</ControlBehavior>
        <MetricType>1</MetricType>
        <Threshold>20</Threshold>
        <Enable>false</Enable>
    </Data>
    <Code>200</Code>
    <Success>true</Success>
</ModifyHotParamRuleResponse>
```

`JSON`格式

```
HTTP/1.1 200 OK
Content-Type:application/json

{
  "Message" : "null",
  "RequestId" : "3FEEAD12-CE22-4EDE-A729-CE94EC070610",
  "Data" : {
    "ParamIdx" : 1,
    "Namespace" : "default",
    "ParamFlowItemList" : [ {
      "ItemValue" : "apple",
      "ItemType" : "String",
      "Threshold" : 20
    } ],
    "StatDurationSec" : 1,
    "BurstCount" : 2,
    "RuleId" : 123,
    "Resource" : "handleService",
    "AppName" : "ahas-demo",
    "MaxQueueingTimeMs" : 3000,
    "ControlBehavior" : 0,
    "MetricType" : 1,
    "Threshold" : 20,
    "Enable" : false
  },
  "Code" : "200",
  "Success" : true
}
```

## 错误码

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|400|IllegalArgument.RuleId|The specified RuleId is invalid.|参数RuleId不合法|
|400|IllegalArgument.MetricType|The specified MetricType is invalid.|参数MetricType不合法|
|400|IllegalArgument.Threshold|The specified Threshold is invalid.|参数Threshold不合法|
|400|IllegalArgument.ParamIdx|The specified ParamIdx is invalid.|参数ParamIdx不合法|
|400|IllegalArgument.ControlBehavior|The specified ControlBehavior is invalid.|参数ControlBehavior不合法|
|400|IllegalArgument.MaxQueueingTimeM|The specified MaxQueueingTimeMs is invalid.|参数MaxQueueingTimeMs不合法|
|400|IllegalArgument.BurstCount|The specified BurstCount is invalid.|参数BurstCount不合法|

访问[错误中心](https://error-center.aliyun.com/status/product/ahas-openapi)查看更多错误码。

