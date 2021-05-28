# CreateSystemRule

调用CreateSystemRule接口创建系统规则。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=ahas-openapi&api=CreateSystemRule&type=RPC&version=2019-09-01)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|CreateSystemRule|系统规定参数。取值：**CreateSystemRule**。 |
|Namespace|String|是|default|命名空间。 |
|AppName|String|是|ahas-demo|应用名，若为EDAS应用，则AppName为EDAS中的App ID，可在EDAS控制台“应用管理\>基本信息”中查看对应的ID。 |
|MetricType|Integer|是|4|统计维度，0表示Load，1表示入口平均RT，2表示线程数，3表示入口总QPS，4表示CPU使用率。 |
|Threshold|Float|是|0.6|阈值。 |
|Enable|Boolean|否|true|是否开启。 |
|AhasRegionId|String|否|cn-hangzhou|地域 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|Message|String|null|错误消息 |
|RequestId|String|3FEEAD12-CE22-4EDE-A729-CE94EC070610|请求ID |
|Data|Object| |业务数据 |
|MetricType|Integer|4|统计维度 |
|Threshold|Float|0.6|阈值 |
|RuleId|Long|123|规则ID |
|Enable|Boolean|true|规则是否开启 |
|Code|String|200|返回码 |
|Success|Boolean|true|是否成功 |

## 示例

请求示例

```
http(s)://[Endpoint]/?Action=CreateSystemRule
&AppName=ahas-demo
&MetricType=4
&Namespace=default
&Threshold=0.6
&<公共请求参数>
```

正常返回示例

`XML`格式

```
HTTP/1.1 200 OK
Content-Type:application/xml

<CreateSystemRuleResponse>
    <Message>null</Message>
    <RequestId>3FEEAD12-CE22-4EDE-A729-CE94EC070610</RequestId>
    <Data>
        <MetricType>4</MetricType>
        <Threshold>0.6</Threshold>
        <RuleId>123</RuleId>
        <Enable>true</Enable>
    </Data>
    <Code>200</Code>
    <Success>true</Success>
</CreateSystemRuleResponse>
```

`JSON`格式

```
HTTP/1.1 200 OK
Content-Type:application/json

{
  "Message" : "null",
  "RequestId" : "3FEEAD12-CE22-4EDE-A729-CE94EC070610",
  "Data" : {
    "MetricType" : 4,
    "Threshold" : 0.6,
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
|400|IllegalArgument.AppName|The specified AppName is invalid.|参数AppName不合法|
|400|IllegalArgument.MetricType|The specified MetricType is invalid.|参数MetricType不合法|
|400|IllegalArgument.Namespace|The specified Namespace is invalid.|参数Namespace不合法|
|400|IllegalArgument.Threshold|The specified Threshold is invalid.|参数Threshold不合法|

访问[错误中心](https://error-center.aliyun.com/status/product/ahas-openapi)查看更多错误码。

