# ListSystemRules

调用ListSystemRules接口获取系统规则。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=ahas-openapi&api=ListSystemRules&type=RPC&version=2019-09-01)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|ListSystemRules|系统规定参数。取值：**ListSystemRules**。 |
|Namespace|String|是|default|命名空间 |
|AppName|String|是|ahas-demo|应用名，若为EDAS应用，则AppName为EDAS中的App ID，可在EDAS控制台“应用管理\>基本信息”中查看对应的ID。 |
|PageIndex|Integer|否|1|当前页码 |
|PageSize|Integer|否|10|每页数据条数 |
|AhasRegionId|String|否|cn-hangzhou|地域 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|Message|String|null|错误信息 |
|RequestId|String|3FEEAD12-CE22-4EDE-A729-CE94EC070610|请求ID |
|Data|Object| |返回数据 |
|PageIndex|Integer|1|当前页码 |
|Datas|Array of Datas| |系统规则列表 |
|AppName|String|ahas-demo|应用名，若为EDAS应用，则AppName为EDAS中的App ID，可在EDAS控制台“应用管理\>基本信息”中查看对应的ID。 |
|Namespace|String|default|命名空间 |
|MetricType|Integer|4|统计维度 |
|Threshold|Float|0.6|阈值 |
|Enable|Boolean|true|是否开启 |
|RuleId|Long|123|规则ID |
|TotalPage|Integer|3|总页数 |
|PageSize|Integer|10|每页数据条数 |
|TotalCount|Integer|23|总数据量 |
|Code|String|200|返回码 |
|Success|Boolean|true|是否成功 |

## 示例

请求示例

```
http(s)://[Endpoint]/?Action=ListSystemRules
&AppName=ahas-demo
&Namespace=default
&<公共请求参数>
```

正常返回示例

`XML`格式

```
HTTP/1.1 200 OK
Content-Type:application/xml

<ListSystemRulesResponse>
    <Message>null</Message>
    <RequestId>3FEEAD12-CE22-4EDE-A729-CE94EC070610</RequestId>
    <Data>
        <PageIndex>1</PageIndex>
        <Datas>
            <AppName>ahas-demo</AppName>
            <Namespace>default</Namespace>
            <MetricType>4</MetricType>
            <Threshold>0.6</Threshold>
            <Enable>true</Enable>
            <RuleId>123</RuleId>
        </Datas>
        <TotalPage>3</TotalPage>
        <PageSize>10</PageSize>
        <TotalCount>23</TotalCount>
    </Data>
    <Code>200</Code>
    <Success>true</Success>
</ListSystemRulesResponse>
```

`JSON`格式

```
HTTP/1.1 200 OK
Content-Type:application/json

{
  "Message" : "null",
  "RequestId" : "3FEEAD12-CE22-4EDE-A729-CE94EC070610",
  "Data" : {
    "PageIndex" : 1,
    "Datas" : [ {
      "AppName" : "ahas-demo",
      "Namespace" : "default",
      "MetricType" : 4,
      "Threshold" : 0.6,
      "Enable" : true,
      "RuleId" : 123
    } ],
    "TotalPage" : 3,
    "PageSize" : 10,
    "TotalCount" : 23
  },
  "Code" : "200",
  "Success" : true
}
```

## 错误码

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|400|IllegalArgument.AppName|The specified AppName is invalid.|参数AppName不合法|
|400|IllegalArgument.Namespace|The specified Namespace is invalid.|参数Namespace不合法|

访问[错误中心](https://error-center.aliyun.com/status/product/ahas-openapi)查看更多错误码。

