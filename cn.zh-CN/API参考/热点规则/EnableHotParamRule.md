# EnableHotParamRule

调用EnableHotParamRule接口开启热点规则。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=ahas-openapi&api=EnableHotParamRule&type=RPC&version=2019-09-01)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|EnableHotParamRule|系统规定参数。取值：EnableHotParamRule。 |
|RuleId|Long|是|123|热点规则ID。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|Code|String|200|返回码 |
|Data|Struct| |返回数据 |
|AppName|String|ahas-demo|应用名，若为EDAS应用，则AppName为EDAS中的App ID，可在EDAS控制台“应用管理\>基本信息”中查看对应的ID。 |
|BurstCount|Integer|2|缓冲请求数 |
|ControlBehavior|Integer|0|流控效果，0表示快速失败，2表示排队等待。 |
|Enable|Boolean|true|规则是否开启 |
|MaxQueueingTimeMs|Integer|3000|流控效果为排队等待时对应的超时时间 |
|MetricType|Integer|0|统计维度，0表示并发数，1表示通过请求数。 |
|Namespace|String|default|命名空间 |
|ParamFlowItemList|Array of ParamFlowItemList| |热点例外项 |
|ItemType|String|String|例外项类型 |
|ItemValue|String|apple|例外项参数值 |
|Threshold|Float|10|例外项阈值 |
|ParamIdx|Integer|1|参数位置索引 |
|Resource|String|handleService|资源名 |
|RuleId|Long|123|热点规则ID |
|StatDurationSec|Long|1|统计周期时间 |
|Threshold|Float|20|单机阈值 |
|Message|String|null|错误信息 |
|RequestId|String|3FEEAD12-CE22-4EDE-A729-CE94EC070610|请求ID |
|Success|Boolean|true|是否成功 |

## 示例

请求示例

```
http(s)://[Endpoint]/?Action=EnableHotParamRule
&RuleId=123
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<EnableHotParamRuleResponse>
  <Message>null</Message>
  <RequestId>3FEEAD12-CE22-4EDE-A729-CE94EC070610</RequestId>
  <Data>
        <MetricType>0</MetricType>
        <RuleId>123</RuleId>
        <Resource>handleService</Resource>
        <MaxQueueingTimeMs>3000</MaxQueueingTimeMs>
        <Namespace>default</Namespace>
        <AppName>ahas-demo</AppName>
        <BurstCount>2</BurstCount>
        <ParamFlowItemList>
              <ItemValue>apple</ItemValue>
              <ItemType>String </ItemType>
              <Threshold>10</Threshold>
        </ParamFlowItemList>
        <ControlBehavior>0</ControlBehavior>
        <StatDurationSec>1</StatDurationSec>
        <Enable>true</Enable>
        <ParamIdx>1</ParamIdx>
        <Threshold>20</Threshold>
  </Data>
  <Code>200</Code>
  <Success>true</Success>
</EnableHotParamRuleResponse>
```

`JSON` 格式

```
{
    "Message":"null",
    "RequestId":"3FEEAD12-CE22-4EDE-A729-CE94EC070610",
    "Data":
    {
        "MetricType":"0",
        "RuleId":"123",
        "Resource":"handleService",
        "MaxQueueingTimeMs":"3000",
        "Namespace":"default",
        "AppName":"ahas-demo",
        "BurstCount":"2",
        "ParamFlowItemList":
        [{
            "ItemValue":"apple",
            "ItemType":"String ",
            "Threshold":"10"
        }],
        "ControlBehavior":"0",
        "StatDurationSec":"1",
        "Enable":"true",
        "ParamIdx":"1",
        "Threshold":"20"
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

