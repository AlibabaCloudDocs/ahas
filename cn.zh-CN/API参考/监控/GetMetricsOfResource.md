# GetMetricsOfResource

调用GetMetricsOfResource接口获取资源metric数据。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=ahas-openapi&api=GetMetricsOfResource&type=RPC&version=2019-09-01)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|GetMetricsOfResource|系统规定参数。取值：**GetMetricsOfResource**。 |
|Namespace|String|是|default|命名空间 |
|AppName|String|是|ahas-demo|应用名，若为EDAS应用，则AppName为EDAS中的App ID，可在EDAS控制台“应用管理\>基本信息”中查看对应的ID。 |
|Resource|String|是|handleService|资源名 |
|StartTime|Long|否|1596081600000|开始时间 |
|EndTime|Long|否|1596081780000|结束时间 |
|AhasRegionId|String|否|cn-hangzhou|地域 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|Message|String|null|错误信息 |
|RequestId|String|3FEEAD12-CE22-4EDE-A729-CE94EC070610|请求ID |
|Data|Object| |返回数据 |
|AppName|String|ahas-demo|应用名，若为EDAS应用，则AppName为EDAS中的App ID，可在EDAS控制台“应用管理\>基本信息”中查看对应的ID。 |
|Resource|String|handleService|资源名 |
|Namespace|String|default|命名空间 |
|InnerMetrics|Array of InnerMetrics| |资源metric数据 |
|RtP99|Float|7|接口RT 99分位数值 |
|SuccessQpsAvg|Float|143|接口success QPS平均值 |
|PassedQpsP99|Float|143|接口paas QPS 99分位数值 |
|RtAvg|Float|6.5|接口RT平均值 |
|Count|Integer|2|机器数 |
|ThreadStd|Float|0|接口并发数标准差值 |
|PassedQpsAvg|Float|143|接口paas QPS平均值 |
|ExceptionP95|Float|0|接口异常QPS 95分位数值 |
|SuccessQpsMax|Float|143|接口success QPS最大值 |
|RtP95|Float|7|接口RT 95分位数值 |
|BlockedQpsMin|Float|86|接口限流QPS最小值 |
|BlockedQps|Float|173|接口集群限流QPS |
|Timestamp|Long|1596593014000|时间戳 |
|ThreadP95|Float|1|接口并发数95分位数值 |
|RtStd|Float|0.7|接口RT 标准差值 |
|PassedQpsMin|Float|143|接口paas QPS最小值 |
|BlockedQpsP99|Float|86|接口限流QPS 99分位数值 |
|PassedQpsMax|Float|143|接口paas QPS最大值 |
|ExceptionMax|Float|0|接口异常QPS最大值 |
|SuccessQps|Float|286|接口集群success QPS |
|SuccessQpsP75|Float|143|接口success QPS 75分位数值 |
|ThreadP75|Float|1|接口并发数75分位数值 |
|SuccessQpsStd|Float|0|接口success QPS 标准差值 |
|ExceptionMin|Float|0|接口异常QPS最小值 |
|PassedQpsP75|Float|143|接口paas QPS 75分位数值 |
|PassedQps|Float|286|接口集群paas QPS |
|ThreadMax|Float|1|接口并发数最大值 |
|SuccessQpsP99|Float|143|接口success QPS 95分位数值 |
|SuccessQpsMin|Float|143|接口success QPS最小值 |
|ThreadP99|Float|1|接口并发数99分位数值 |
|ExceptionStd|Float|0|接口异常QPS 标准差值 |
|BlockedQpsP95|Float|86|接口限流QPS 95分位数值 |
|Thread|Float|2|接口集群并发数 |
|ThreadMin|Float|1|接口并发数最小值 |
|RtMin|Float|6.5|接口RT最小值 |
|BlockedQpsAvg|Float|86|接口限流QPS平均值 |
|ThreadAvg|Float|1|接口并发数平均值 |
|BlockedQpsP75|Float|86|接口限流QPS 75分位数值 |
|RtP75|Float|7|接口RT 75分位数值 |
|ExceptionP99|Float|0|接口异常QPS 99分位数值 |
|ExceptionP75|Float|0|接口异常QPS 75分位数值 |
|SuccessQpsP95|Float|143|接口success QPS 95分位数值 |
|Rt|Float|6.5|接口集群平均RT |
|PassedQpsP95|Float|143|接口paas QPS 95分位数值 |
|RtMax|Float|7|接口RT最大值 |
|BlockedQpsStd|Float|0|接口限流QPS 标准差值 |
|BlockedQpsMax|Float|86|接口限流QPS最大值 |
|Exception|Float|0|接口集群异常QPS |
|ExceptionAvg|Float|0|接口异常QPS平均值 |
|PassedQpsStd|Float|0|接口paas QPS标准差值 |
|Code|String|200|返回码 |
|Success|Boolean|true|是否成功 |

## 示例

请求示例

```
http(s)://[Endpoint]/?Action=GetMetricsOfResource
&AppName=ahas-demo
&Namespace=default
&Resource=handleService
&<公共请求参数>
```

正常返回示例

`XML`格式

```
HTTP/1.1 200 OK
Content-Type:application/xml

<GetMetricsOfResourceResponse>
<Message>null</Message>
<RequestId>3FEEAD12-CE22-4EDE-A729-CE94EC070610</RequestId>
<Data>
    <Resource>handleService</Resource>
    <Namespace>default</Namespace>
    <AppName>ahas-demo</AppName>
    <InnerMetrics>
        <BlockedQps>173</BlockedQps>
        <PassedQpsMax>143</PassedQpsMax>
        <Count>2</Count>
        <ThreadMax>1</ThreadMax>
        <ThreadP75>1</ThreadP75>
        <SuccessQpsP75>143</SuccessQpsP75>
        <ExceptionP95>0</ExceptionP95>
        <PassedQps>286</PassedQps>
        <RtMax>7</RtMax>
        <ThreadAvg>1</ThreadAvg>
        <ThreadMin>1</ThreadMin>
        <BlockedQpsP75>86</BlockedQpsP75>
        <BlockedQpsAvg>86</BlockedQpsAvg>
        <BlockedQpsMin>86</BlockedQpsMin>
        <PassedQpsP99>143</PassedQpsP99>
        <RtAvg>6.5</RtAvg>
        <RtMin>6.5</RtMin>
        <PassedQpsP95>143</PassedQpsP95>
        <ExceptionP99>0</ExceptionP99>
        <RtP75>7</RtP75>
        <ExceptionStd>0</ExceptionStd>
        <PassedQpsStd>0</PassedQpsStd>
        <SuccessQpsStd>0</SuccessQpsStd>
        <BlockedQpsMax>86</BlockedQpsMax>
        <SuccessQps>286</SuccessQps>
        <ThreadStd>0</ThreadStd>
        <Timestamp>1596593014000</Timestamp>
        <SuccessQpsP99>143</SuccessQpsP99>
        <ExceptionP75>0</ExceptionP75>
        <ThreadP99>1</ThreadP99>
        <SuccessQpsP95>143</SuccessQpsP95>
        <ThreadP95>1</ThreadP95>
        <RtStd>0.7</RtStd>
        <Rt>6.5</Rt>
        <BlockedQpsP95>86</BlockedQpsP95>
        <BlockedQpsP99>86</BlockedQpsP99>
        <PassedQpsAvg>143</PassedQpsAvg>
        <PassedQpsMin>143</PassedQpsMin>
        <ExceptionAvg>0</ExceptionAvg>
        <ExceptionMin>0</ExceptionMin>
        <Exception>0</Exception>
        <SuccessQpsAvg>143</SuccessQpsAvg>
        <SuccessQpsMin>143</SuccessQpsMin>
        <PassedQpsP75>143</PassedQpsP75>
        <Thread>2</Thread>
        <RtP95>7</RtP95>
        <RtP99>7</RtP99>
        <BlockedQpsStd>0</BlockedQpsStd>
        <ExceptionMax>0</ExceptionMax>
        <SuccessQpsMax>143</SuccessQpsMax>
    </InnerMetrics>
</Data>
<Code>200</Code>
<Success>true</Success>
</GetMetricsOfResourceResponse>
```

`JSON`格式

```
HTTP/1.1 200 OK
Content-Type:application/json

{
  "Message" : "null",
  "RequestId" : "3FEEAD12-CE22-4EDE-A729-CE94EC070610",
  "Data" : {
    "Resource" : "handleService",
    "Namespace" : "default",
    "AppName" : "ahas-demo",
    "InnerMetrics" : [ {
      "BlockedQps" : "173",
      "PassedQpsMax" : "143",
      "Count" : "2",
      "ThreadMax" : "1",
      "ThreadP75" : "1",
      "SuccessQpsP75" : "143",
      "ExceptionP95" : "0",
      "PassedQps" : "286",
      "RtMax" : "7",
      "ThreadAvg" : "1",
      "ThreadMin" : "1",
      "BlockedQpsP75" : "86",
      "BlockedQpsAvg" : "86",
      "BlockedQpsMin" : "86",
      "PassedQpsP99" : "143",
      "RtAvg" : "6.5",
      "RtMin" : "6.5",
      "PassedQpsP95" : "143",
      "ExceptionP99" : "0",
      "RtP75" : "7",
      "ExceptionStd" : "0",
      "PassedQpsStd" : "0",
      "SuccessQpsStd" : "0",
      "BlockedQpsMax" : "86",
      "SuccessQps" : "286",
      "ThreadStd" : "0",
      "Timestamp" : "1596593014000",
      "SuccessQpsP99" : "143",
      "ExceptionP75" : "0",
      "ThreadP99" : "1",
      "SuccessQpsP95" : "143",
      "ThreadP95" : "1",
      "RtStd" : "0.7",
      "Rt" : "6.5",
      "BlockedQpsP95" : "86",
      "BlockedQpsP99" : "86",
      "PassedQpsAvg" : "143",
      "PassedQpsMin" : "143",
      "ExceptionAvg" : "0",
      "ExceptionMin" : "0",
      "Exception" : "0",
      "SuccessQpsAvg" : "143",
      "SuccessQpsMin" : "143",
      "PassedQpsP75" : "143",
      "Thread" : "2",
      "RtP95" : "7",
      "RtP99" : "7",
      "BlockedQpsStd" : "0",
      "ExceptionMax" : "0",
      "SuccessQpsMax" : "143"
    } ]
  },
  "Code" : "200",
  "Success" : "true"
}
```

## 错误码

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|400|IllegalArgument.AppName|The specified AppName is invalid.|参数AppName不合法|
|400|IllegalArgument.Namespace|The specified Namespace is invalid.|参数Namespace不合法|
|400|IllegalArgument.Resource|The specified Resource is invalid.|参数Resource不合法|

访问[错误中心](https://error-center.aliyun.com/status/product/ahas-openapi)查看更多错误码。

