# CreateDegradeRule

调用CreateDegradeRule接口创建降级规则。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=ahas-openapi&api=CreateDegradeRule&type=RPC&version=2019-09-01)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|CreateDegradeRule|系统规定参数。取值：**CreateDegradeRule**。 |
|Namespace|String|是|default|AHAS命名空间，默认为default，可以在控制台上创建不同namespace用于逻辑隔离。 |
|AppName|String|是|ahas-demo|应用名（避免中文命名），若为EDAS应用，则AppName为EDAS中的App ID，可在EDAS控制台“应用管理\>基本信息”中查看对应的ID。 |
|Resource|String|是|handleService|资源名。 |
|Strategy|Integer|是|0|阈值类型，即降级的策略，取值为0时表示按慢调用比例降级，取值为1时表示按异常比例降级。 |
|Threshold|Float|是|0.6|阈值类型所对应的降级阈值，超过该值时会触发接口的降级。 |
|Enable|Boolean|否|true|规则是否开启。默认为false。 |
|RecoveryTimeoutMs|Integer|是|5000|熔断时长。在该时间段内，该接口的请求都会快速失败。 |
|StatDurationMs|Integer|否|2000|统计窗口时长，单位MS。默认值为1000。 |
|SlowRtMs|Integer|否|2000|慢调用RT。请求的响应时间超过该值时统计为慢调用。阈值类型为“慢调用比例”时需设置该字段。 |
|MinRequestAmount|Integer|否|10|触发熔断的最小请求数目，若当前统计窗口请求数小于此值，即使达到熔断条件规则也不会触发。默认值为5。 |
|HalfOpenBaseAmountPerStep|Integer|否|5|熔断恢复每步最小通过数目，默认值为5。 |
|HalfOpenRecoveryStepNum|Integer|否|1|熔断恢复阶段数，默认值为1。 |
|AhasRegionId|String|否|cn-hangzhou|地域 |

详细参数说明参照文档[降级规则](https://help.aliyun.com/document_detail/101078.html)

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|Message|String|null|错误信息。 |
|RequestId|String|3FEEAD12-CE22-4EDE-A729-CE94EC070610|请求Request ID。 |
|Data|Object| |规则数据。 |
|SlowRtMs|Integer|2000|慢调用RT。 |
|HalfOpenRecoveryStepNum|Integer|1|熔断恢复阶段数。 |
|Namespace|String|default|命名空间。 |
|StatDurationMs|Integer|2000|统计窗口时长。 |
|RuleId|Long|1|规则ID。 |
|Strategy|Integer|0|阈值类型。 |
|Resource|String|handleService|资源名。 |
|AppName|String|ahas-demo|应用名，若为EDAS应用，则AppName为EDAS中的App ID，可在EDAS控制台“应用管理\>基本信息”中查看对应的ID。 |
|HalfOpenBaseAmountPerStep|Integer|5|熔断恢复每步最小通过数目，默认值为5。 |
|RecoveryTimeoutMs|Integer|5000|熔断时长。 |
|MinRequestAmount|Integer|10|触发熔断的最小请求数。 |
|Threshold|Float|0.6|降级阈值。 |
|Enable|Boolean|true|规则是否开启。 |
|Code|String|200|错误码。 |
|Success|Boolean|true|是否成功。 |

## 示例

请求示例

```
http(s)://[Endpoint]/?Action=CreateDegradeRule
&AppName=ahas-demo
&Namespace=default
&RecoveryTimeoutMs=5000
&Resource=handleService
&Strategy=0
&Threshold=0.6
&<公共请求参数>
```

正常返回示例

`XML`格式

```
HTTP/1.1 200 OK
Content-Type:application/xml

<CreateDegradeRuleResponse>
    <Message>null</Message>
    <RequestId>3FEEAD12-CE22-4EDE-A729-CE94EC070610</RequestId>
    <Data>
        <SlowRtMs>2000</SlowRtMs>
        <HalfOpenRecoveryStepNum>1</HalfOpenRecoveryStepNum>
        <Namespace>default</Namespace>
        <StatDurationMs>2000</StatDurationMs>
        <RuleId>1</RuleId>
        <Strategy>0</Strategy>
        <Resource>handleService</Resource>
        <AppName>ahas-demo</AppName>
        <HalfOpenBaseAmountPerStep>5</HalfOpenBaseAmountPerStep>
        <RecoveryTimeoutMs>5000</RecoveryTimeoutMs>
        <MinRequestAmount>10</MinRequestAmount>
        <Threshold>0.6</Threshold>
        <Enable>true</Enable>
    </Data>
    <Code>200</Code>
    <Success>true</Success>
</CreateDegradeRuleResponse>
```

`JSON`格式

```
HTTP/1.1 200 OK
Content-Type:application/json

{
  "Message" : "null",
  "RequestId" : "3FEEAD12-CE22-4EDE-A729-CE94EC070610",
  "Data" : {
    "SlowRtMs" : 2000,
    "HalfOpenRecoveryStepNum" : 1,
    "Namespace" : "default",
    "StatDurationMs" : 2000,
    "RuleId" : 1,
    "Strategy" : 0,
    "Resource" : "handleService",
    "AppName" : "ahas-demo",
    "HalfOpenBaseAmountPerStep" : 5,
    "RecoveryTimeoutMs" : 5000,
    "MinRequestAmount" : 10,
    "Threshold" : 0.6,
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
|400|IllegalArgument.HalfOpenBaseAmountPerStep|The specified HalfOpenBaseAmountPerStep is invalid.|参数HalfOpenBaseAmountPerStep不合法|
|400|IllegalArgument.HalfOpenRecoveryStepNum|The specified HalfOpenRecoveryStepNum is invalid.|参数HalfOpenRecoveryStepNum不合法|
|400|IllegalArgument.MinRequestAmount|The specified MinRequestAmount is invalid.|参数MinRequestAmount不合法|
|400|IllegalArgument.Namespace|The specified Namespace is invalid.|参数Namespace不合法|
|400|IllegalArgument.RecoveryTimeoutMs|The specified RecoveryTimeoutMs is invalid.|参数RecoveryTimeoutMs不合法|
|400|IllegalArgument.Resource|The specified Resource is invalid.|参数Resource不合法|
|400|IllegalArgument.SlowRtMS|The specified SlowRtMs is invalid.|参数SlowRtMs不合法|
|400|IllegalArgument.StatDurationMs|The specified StatDurationMs is invalid.|参数StatDurationMs不合法|
|400|IllegalArgument.Strategy|The specified Strategy is invalid.|参数Strategy不合法|
|400|IllegalArgument.Threshold|The specified Threshold is invalid.|参数Threshold不合法|

访问[错误中心](https://error-center.aliyun.com/status/product/ahas-openapi)查看更多错误码。

