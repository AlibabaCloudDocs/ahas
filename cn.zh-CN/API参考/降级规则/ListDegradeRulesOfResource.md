# ListDegradeRulesOfResource

调用ListDegradeRulesOfResource接口获取资源对应的降级规则。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=ahas-openapi&api=ListDegradeRulesOfResource&type=RPC&version=2019-09-01)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|ListDegradeRulesOfResource|系统规定参数。取值：**ListDegradeRulesOfResource**。 |
|Namespace|String|是|default|命名空间 |
|AppName|String|是|ahas-demo|应用名，若为EDAS应用，则AppName为EDAS中的App ID，可在EDAS控制台“应用管理\>基本信息”中查看对应的ID。 |
|Resource|String|是|handleServiceA|资源名 |
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
|Datas|Array of Datas| |降级规则列表 |
|SlowRtMs|Integer|2000|慢调用RT |
|HalfOpenRecoveryStepNum|Integer|1|熔断恢复阶段数 |
|Namespace|String|default|命名空间 |
|StatDurationMs|Integer|2000|统计窗口时长 |
|RuleId|Long|123|规则ID |
|Strategy|Integer|0|阈值类型 |
|Resource|String|handleSerivice|接口资源名 |
|AppName|String|ahas-demo|应用名，若为EDAS应用，则AppName为EDAS中的App ID，可在EDAS控制台“应用管理\>基本信息”中查看对应的ID。 |
|HalfOpenBaseAmountPerStep|Integer|5|熔断恢复每步最小通过数目，默认值为5。 |
|RecoveryTimeoutMs|Integer|5000|熔断时长 |
|MinRequestAmount|Integer|10|触发熔断的最小请求数 |
|Threshold|Float|0.6|降级阈值 |
|Enable|Boolean|false|规则是否开启 |
|TotalPage|Integer|3|总页数 |
|PageSize|Integer|10|每页数据条数 |
|TotalCount|Integer|23|数据总数 |
|Code|String|200|返回码 |
|Success|Boolean|true|是否成功 |

## 示例

请求示例

```
http(s)://[Endpoint]/?Action=ListDegradeRulesOfResource
&AppName=ahas-demo
&Namespace=default
&Resource=handleServiceA
&<公共请求参数>
```

正常返回示例

`XML`格式

```
HTTP/1.1 200 OK
Content-Type:application/xml

<ListDegradeRulesOfResourceResponse>
    <Message>null</Message>
    <RequestId>3FEEAD12-CE22-4EDE-A729-CE94EC070610</RequestId>
    <Data>
        <PageIndex>1</PageIndex>
        <Datas>
            <SlowRtMs>2000</SlowRtMs>
            <HalfOpenRecoveryStepNum>1</HalfOpenRecoveryStepNum>
            <Namespace>default</Namespace>
            <StatDurationMs>2000</StatDurationMs>
            <RuleId>123</RuleId>
            <Strategy>0</Strategy>
            <Resource>handleSerivice</Resource>
            <AppName>ahas-demo</AppName>
            <HalfOpenBaseAmountPerStep>5</HalfOpenBaseAmountPerStep>
            <RecoveryTimeoutMs>5000</RecoveryTimeoutMs>
            <MinRequestAmount>10</MinRequestAmount>
            <Threshold>0.6</Threshold>
            <Enable>false</Enable>
        </Datas>
        <TotalPage>3</TotalPage>
        <PageSize>10</PageSize>
        <TotalCount>23</TotalCount>
    </Data>
    <Code>200</Code>
    <Success>true</Success>
</ListDegradeRulesOfResourceResponse>
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
      "SlowRtMs" : 2000,
      "HalfOpenRecoveryStepNum" : 1,
      "Namespace" : "default",
      "StatDurationMs" : 2000,
      "RuleId" : 123,
      "Strategy" : 0,
      "Resource" : "handleSerivice",
      "AppName" : "ahas-demo",
      "HalfOpenBaseAmountPerStep" : 5,
      "RecoveryTimeoutMs" : 5000,
      "MinRequestAmount" : 10,
      "Threshold" : 0.6,
      "Enable" : false
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
|400|IllegalArgument.Resource|The specified Resource is invalid.|参数Resource不合法|

访问[错误中心](https://error-center.aliyun.com/status/product/ahas-openapi)查看更多错误码。

