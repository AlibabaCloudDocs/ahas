# DisableDegradeRule

调用DisableDegradeRule接口关闭降级规则。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=ahas-openapi&api=DisableDegradeRule&type=RPC&version=2019-09-01)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|DisableDegradeRule|系统规定参数。取值：**DisableDegradeRule**。 |
|RuleId|Long|是|123|降级规则ID。 |
|AhasRegionId|String|否|cn-hangzhou|地域 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|Message|String|null|错误信息 |
|RequestId|String|3FEEAD12-CE22-4EDE-A729-CE94EC070610|请求ID |
|Data|Object| |业务数据 |
|SlowRtMs|Integer|2000|慢调用RT |
|HalfOpenRecoveryStepNum|Integer|1|熔断恢复阶段数 |
|Namespace|String|default|命名空间 |
|StatDurationMs|Integer|2000|统计窗口时长 |
|RuleId|Long|123|降级规则ID |
|Strategy|Integer|0|阈值类型 |
|Resource|String|handleService|资源名 |
|AppName|String|ahas-demo|应用名，若为EDAS应用，则AppName为EDAS中的App ID，可在EDAS控制台“应用管理\>基本信息”中查看对应的ID。 |
|HalfOpenBaseAmountPerStep|Integer|5|熔断恢复每步最小通过数目 |
|RecoveryTimeoutMs|Integer|5000|熔断时长 |
|MinRequestAmount|Integer|10|触发熔断的最小请求数目 |
|Threshold|Float|0.6|阈值类型所对应的降级阈值 |
|Enable|Boolean|false|规则是否启用 |
|Code|String|200|返回码 |
|Success|Boolean|true|是否成功 |

## 示例

请求示例

```
http(s)://[Endpoint]/?Action=DisableDegradeRule
&RuleId=123
&<公共请求参数>
```

正常返回示例

`XML`格式

```
HTTP/1.1 200 OK
Content-Type:application/xml

<DisableDegradeRuleResponse>
    <Message>null</Message>
    <RequestId>3FEEAD12-CE22-4EDE-A729-CE94EC070610</RequestId>
    <Data>
        <SlowRtMs>2000</SlowRtMs>
        <HalfOpenRecoveryStepNum>1</HalfOpenRecoveryStepNum>
        <Namespace>default </Namespace>
        <StatDurationMs>2000</StatDurationMs>
        <RuleId>123</RuleId>
        <Strategy>0</Strategy>
        <Resource>handleService</Resource>
        <AppName>ahas-demo</AppName>
        <HalfOpenBaseAmountPerStep>5</HalfOpenBaseAmountPerStep>
        <RecoveryTimeoutMs>5000</RecoveryTimeoutMs>
        <MinRequestAmount>10</MinRequestAmount>
        <Threshold>0.6</Threshold>
        <Enable>false</Enable>
    </Data>
    <Code>200</Code>
    <Success>true</Success>
</DisableDegradeRuleResponse>
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
    "Namespace" : "default ",
    "StatDurationMs" : 2000,
    "RuleId" : 123,
    "Strategy" : 0,
    "Resource" : "handleService",
    "AppName" : "ahas-demo",
    "HalfOpenBaseAmountPerStep" : 5,
    "RecoveryTimeoutMs" : 5000,
    "MinRequestAmount" : 10,
    "Threshold" : 0.6,
    "Enable" : false
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

