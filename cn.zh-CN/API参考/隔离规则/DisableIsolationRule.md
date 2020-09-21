# DisableIsolationRule

调用DisableIsolationRule接口关闭隔离规则。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=ahas-openapi&api=DisableIsolationRule&type=RPC&version=2019-09-01)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|DisableIsolationRule|系统规定参数。取值：DisableIsolationRule。 |
|RuleId|Long|是|123|隔离规则ID。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|Code|String|200|返回码 |
|Data|Struct| |隔离规则数据 |
|AppName|String|ahas-demo|应用名，若为EDAS应用，则AppName为EDAS中的App ID，可在EDAS控制台“应用管理\>基本信息”中查看对应的ID。 |
|Enable|Boolean|false|规则是否启用 |
|LimitOrigin|String|default|来源应用 |
|Namespace|String|default|命名空间 |
|RefResource|String|handleServiceB|关联接口名、callstack入口名 |
|RelationStrategy|Integer|0|统计维度 |
|Resource|String|handleServiceA|资源名 |
|RuleId|Long|123|隔离规则ID |
|Threshold|Float|10|并发数阈值 |
|Message|String|null|错误信息 |
|RequestId|String|3FEEAD12-CE22-4EDE-A729-CE94EC070610|请求ID |
|Success|Boolean|true|是否成功 |

## 示例

请求示例

```
http(s)://[Endpoint]/?Action=DisableIsolationRule
&RuleId=123
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<DisableIsolationRuleResponse>
  <Message>null</Message>
  <RequestId>3FEEAD12-CE22-4EDE-A729-CE94EC070610</RequestId>
  <Data>
        <RefResource>handleServiceB</RefResource>
        <RuleId>123</RuleId>
        <Resource>handleServiceA</Resource>
        <Enable>false</Enable>
        <RelationStrategy>0</RelationStrategy>
        <LimitOrigin>default</LimitOrigin>
        <Namespace>default</Namespace>
        <AppName>ahas-demo</AppName>
        <Threshold>10</Threshold>
  </Data>
  <Code>200</Code>
  <Success>true</Success>
</DisableIsolationRuleResponse>
```

`JSON` 格式

```
{
    "Message":"null",
    "RequestId":"3FEEAD12-CE22-4EDE-A729-CE94EC070610",
    "Data":
    {
        "RefResource":"handleServiceB",
        "RuleId":"123",
        "Resource":"handleServiceA",
        "Enable":"false",
        "RelationStrategy":"0",
        "LimitOrigin":"default",
        "Namespace":"default",
        "AppName":"ahas-demo",
        "Threshold":"10"
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

