# EnableIsolationRule

调用EnableIsolationRule接口开启隔离规则。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=ahas-openapi&api=EnableIsolationRule&type=RPC&version=2019-09-01)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|EnableIsolationRule|系统规定参数。取值：**EnableIsolationRule**。 |
|RuleId|Long|是|123|隔离规则ID。 |
|AhasRegionId|String|否|cn-hangzhou|地域 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|Message|String|null|错误信息 |
|RequestId|String|3FEEAD12-CE22-4EDE-A729-CE94EC070610|请求ID |
|Data|Object| |返回数据 |
|RelationStrategy|Integer|0|统计维度 |
|Resource|String|handleServiceA|接口资源名 |
|AppName|String|ahas-demo|应用名，若为EDAS应用，则AppName为EDAS中的App ID，可在EDAS控制台“应用管理\>基本信息”中查看对应的ID。 |
|RefResource|String|handleServiceB|关联接口名、callstack入口名 |
|Namespace|String|default|命名空间 |
|LimitOrigin|String|default|来源应用 |
|Threshold|Float|30|并发数阈值 |
|RuleId|Long|123|规则ID |
|Enable|Boolean|true|规则是否开启 |
|Code|String|200|返回码 |
|Success|Boolean|true|是否成功 |

## 示例

请求示例

```
http(s)://[Endpoint]/?Action=EnableIsolationRule
&<公共请求参数>
```

正常返回示例

`XML`格式

```
HTTP/1.1 200 OK
Content-Type:application/xml

<EnableIsolationRuleResponse>
    <Message>null</Message>
    <RequestId>3FEEAD12-CE22-4EDE-A729-CE94EC070610</RequestId>
    <Data>
        <RelationStrategy>0</RelationStrategy>
        <Resource>handleServiceA</Resource>
        <AppName>ahas-demo</AppName>
        <RefResource>handleServiceB</RefResource>
        <Namespace>default</Namespace>
        <LimitOrigin>default</LimitOrigin>
        <Threshold>30</Threshold>
        <RuleId>123</RuleId>
        <Enable>true</Enable>
    </Data>
    <Code>200</Code>
    <Success>true</Success>
</EnableIsolationRuleResponse>
```

`JSON`格式

```
HTTP/1.1 200 OK
Content-Type:application/json

{
  "Message" : "null",
  "RequestId" : "3FEEAD12-CE22-4EDE-A729-CE94EC070610",
  "Data" : {
    "RelationStrategy" : 0,
    "Resource" : "handleServiceA",
    "AppName" : "ahas-demo",
    "RefResource" : "handleServiceB",
    "Namespace" : "default",
    "LimitOrigin" : "default",
    "Threshold" : 30,
    "RuleId" : 123,
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

访问[错误中心](https://error-center.aliyun.com/status/product/ahas-openapi)查看更多错误码。

