# ModifyIsolationRule

调用ModifyIsolationRule接口修改隔离规则。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=ahas-openapi&api=ModifyIsolationRule&type=RPC&version=2019-09-01)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|ModifyIsolationRule|系统规定参数。取值：ModifyIsolationRule。 |
|RelationStrategy|Integer|是|0|统计维度，0表示当前接口，1表示关联接口，2表示链路入口。 |
|RuleId|Long|是|123|隔离规则ID。 |
|Threshold|Float|是|10|并发数阈值。 |
|LimitOrigin|String|否|default|来源应用。 |
|RefResource|String|否|handleServiceB|关联接口名、callstack入口名，当统计维度为关联接口或链路入口时需设置该值。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|Code|String|200|返回码 |
|Data|Struct| |返回数据 |
|AppName|String|ahas-demo|应用名，若为EDAS应用，则AppName为EDAS中的App ID，可在EDAS控制台“应用管理\>基本信息”中查看对应的ID。 |
|Enable|Boolean|true|规则是否开启 |
|LimitOrigin|String|default|来源应用 |
|Namespace|String|default|命名空间 |
|RefResource|String|handleServiceB|关联接口名、callstack入口名 |
|RelationStrategy|Integer|0|统计维度 |
|Resource|String|handleServiceA|资源名 |
|RuleId|Long|123|规则ID |
|Threshold|Float|10|并发数阈值 |
|Message|String|null|错误信息 |
|RequestId|String|3FEEAD12-CE22-4EDE-A729-CE94EC070610|请求ID |
|Success|Boolean|true|是否成功 |

## 示例

请求示例

```
http(s)://[Endpoint]/?Action=ModifyIsolationRule
&RelationStrategy=0
&RuleId=123
&Threshold=10
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<ModifyIsolationRuleResponse>
  <Message>null</Message>
  <RequestId>3FEEAD12-CE22-4EDE-A729-CE94EC070610</RequestId>
  <Data>
        <RefResource>handleServiceB</RefResource>
        <RuleId>123</RuleId>
        <Resource>handleServiceA</Resource>
        <Enable>true</Enable>
        <RelationStrategy>0</RelationStrategy>
        <LimitOrigin>default</LimitOrigin>
        <Namespace>default</Namespace>
        <AppName>ahas-demo</AppName>
        <Threshold>10</Threshold>
  </Data>
  <Code>200</Code>
  <Success>true</Success>
</ModifyIsolationRuleResponse>
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
        "Enable":"true",
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
|400|IllegalArgument.RelationStrategy|The specified RelationStrategy is invalid.|参数RelationStrategy不合法|
|400|IllegalArgument.Threshold|The specified Threshold is invalid.|参数Threshold不合法|
|400|IllegalArgument.RefResource|The specified RefResource is invalid.|参数RefResource不合法|

访问[错误中心](https://error-center.aliyun.com/status/product/ahas-openapi)查看更多错误码。

