# CreateHotParamItems

调用CreateHotParamItems接口创建热点规则例外项。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=ahas-openapi&api=CreateHotParamItems&type=RPC&version=2019-09-01)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|CreateHotParamItems|系统规定参数。取值：**CreateHotParamItems**。 |
|RuleId|Long|是|123|热点规则ID |
|Items|String|是|\[\{"itemType":"String","itemValue":"apple","threshold":50.0\},\{"itemType":"String","itemValue":"orange","threshold":20.0\}\]|热点例外项 |
|AhasRegionId|String|否|cn-hangzhou|地域 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|Message|String|null|错误信息 |
|RequestId|String|3FEEAD12-CE22-4EDE-A729-CE94EC070610|请求Request ID |
|Data|Object| |数据 |
|ParamIdx|Integer|1|参数位置索引 |
|Namespace|String|default|命名空间 |
|ParamFlowItemList|Array of ParamFlowItemList| |例外项 |
|ItemValue|String|apple|例外项参数值 |
|ItemType|String|String|例外项类型 |
|Threshold|Float|10|例外项阈值 |
|StatDurationSec|Long|1|统计周期时间 |
|BurstCount|Integer|2|缓冲请求数 |
|RuleId|Long|123|规则ID |
|Resource|String|handleService|资源名 |
|AppName|String|ahas-demo|应用名，若为EDAS应用，则AppName为EDAS中的App ID，可在EDAS控制台“应用管理\>基本信息”中查看对应的ID。 |
|MaxQueueingTimeMs|Integer|3000|流控效果为排队等待时对应的超时时间。 |
|ControlBehavior|Integer|0|流控效果，0表示快速失败，2表示排队等待。 |
|MetricType|Integer|1|统计维度，0表示并发数，1表示通过请求数。 |
|Threshold|Float|50|单机阈值 |
|Enable|Boolean|true|规则是否开启 |
|Code|String|200|返回码，success=true时返回200，否则返回对应的错误码。 |
|Success|Boolean|true|是否成功 |

## 示例

请求示例

```
http(s)://[Endpoint]/?Action=CreateHotParamItems
&RuleId=123
&<公共请求参数>
```

正常返回示例

`XML`格式

```
HTTP/1.1 200 OK
Content-Type:application/xml

<CreateHotParamItemsResponse>
    <Message>null</Message>
    <RequestId>3FEEAD12-CE22-4EDE-A729-CE94EC070610</RequestId>
    <Data>
        <ParamIdx>1</ParamIdx>
        <Namespace>default</Namespace>
        <ParamFlowItemList>
            <ItemValue>apple</ItemValue>
            <ItemType>String</ItemType>
            <Threshold>10</Threshold>
        </ParamFlowItemList>
        <StatDurationSec>1</StatDurationSec>
        <BurstCount>2</BurstCount>
        <RuleId>123</RuleId>
        <Resource>handleService</Resource>
        <AppName>ahas-demo</AppName>
        <MaxQueueingTimeMs>3000</MaxQueueingTimeMs>
        <ControlBehavior>0</ControlBehavior>
        <MetricType>1</MetricType>
        <Threshold>50</Threshold>
        <Enable>true</Enable>
    </Data>
    <Code>200</Code>
    <Success>true</Success>
</CreateHotParamItemsResponse>
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
      "Threshold" : 10
    } ],
    "StatDurationSec" : 1,
    "BurstCount" : 2,
    "RuleId" : 123,
    "Resource" : "handleService",
    "AppName" : "ahas-demo",
    "MaxQueueingTimeMs" : 3000,
    "ControlBehavior" : 0,
    "MetricType" : 1,
    "Threshold" : 50,
    "Enable" : true
  },
  "Code" : "200",
  "Success" : true
}
```

## 错误码

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|400|IllegalArgument.RuleId|The specified RuleId is invalid.|参数RuleId不合法|
|400|IllegalArgument.ParamItems|The specified Items is invalid.|参数Items不合法|

访问[错误中心](https://error-center.aliyun.com/status/product/ahas-openapi)查看更多错误码。

