# CreateIsolationRule

调用CreateIsolationRule接口创建隔离规则。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=ahas-openapi&api=CreateIsolationRule&type=RPC&version=2019-09-01)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|CreateIsolationRule|系统规定参数。取值：**CreateIsolationRule**。 |
|Namespace|String|是|default|命名空间。 |
|AppName|String|是|ahas-demo|应用名，若为EDAS应用，则AppName为EDAS中的App ID，可在EDAS控制台“应用管理\>基本信息”中查看对应的ID。 |
|RelationStrategy|Integer|是|0|统计维度，0表示当前接口，1表示关联接口，2表示链路入口。 |
|Threshold|Float|是|10|并发数阈值。 |
|Enable|Boolean|否|true|是否开启，默认为false。 |
|Resource|String|是|handleServiceA|资源名。 |
|LimitOrigin|String|否|default|来源应用，默认为default。 |
|RefResource|String|否|handleServiceB|关联接口名、callstack入口名，当统计维度为关联接口或链路入口时需设置该值。 |
|AhasRegionId|String|否|cn-hangzhou|地域 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|Message|String|null|错误信息 |
|RequestId|String|3FEEAD12-CE22-4EDE-A729-CE94EC070610|请求ID |
|Data|Object| |隔离规则数据 |
|RelationStrategy|Integer|0|统计维度 |
|Resource|String|handleServiceA|接口资源名 |
|AppName|String|ahas-demo|应用名，若为EDAS应用，则AppName为EDAS中的App ID，可在EDAS控制台“应用管理\>基本信息”中查看对应的ID。 |
|RefResource|String|handleServiceB|关联接口名、callstack入口名 |
|Namespace|String|default|命名空间 |
|LimitOrigin|String|default|来源应用 |
|Threshold|Float|10|并发数阈值 |
|RuleId|Long|123|隔离规则ID |
|Enable|Boolean|true|是否开启 |
|Code|String|200|返回码 |
|Success|Boolean|true|是否成功 |

## 示例

请求示例

```
http(s)://[Endpoint]/?Action=CreateIsolationRule
&AppName=ahas-demo
&Namespace=default
&RelationStrategy=0
&Resource=handleServiceA
&Threshold=10
&<公共请求参数>
```

正常返回示例

`XML`格式

```
HTTP/1.1 200 OK
Content-Type:application/xml

<CreateIsolationRuleResponse>
    <Message>null</Message>
    <RequestId>3FEEAD12-CE22-4EDE-A729-CE94EC070610</RequestId>
    <Data>
        <RelationStrategy>0</RelationStrategy>
        <Resource>handleServiceA</Resource>
        <AppName>ahas-demo</AppName>
        <RefResource>handleServiceB</RefResource>
        <Namespace>default</Namespace>
        <LimitOrigin>default</LimitOrigin>
        <Threshold>10</Threshold>
        <RuleId>123</RuleId>
        <Enable>true</Enable>
    </Data>
    <Code>200</Code>
    <Success>true</Success>
</CreateIsolationRuleResponse>
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
    "Threshold" : 10,
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
|400|IllegalArgument.Namespace|The specified Namespace is invalid.|参数Namespace不合法|
|400|IllegalArgument.AppName|The specified AppName is invalid.|参数AppName不合法|
|400|IllegalArgument.RelationStrategy|The specified RelationStrategy is invalid.|参数RelationStrategy不合法|
|400|IllegalArgument.RefResource|The specified RefResource is invalid.|参数RefResource不合法|
|400|IllegalArgument.Resource|The specified Resource is invalid.|参数Resource不合法|
|400|IllegalArgument.Threshold|The specified Threshold is invalid.|参数Threshold不合法|

访问[错误中心](https://error-center.aliyun.com/status/product/ahas-openapi)查看更多错误码。

