# GetMetricsOfApp

调用GetMetricsOfApp接口获取应用监控指标。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=ahas-openapi&api=GetMetricsOfApp&type=RPC&version=2019-09-01)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|GetMetricsOfApp|系统规定参数。取值：GetMetricsOfApp。 |
|AppName|String|是|ahas-demo|应用名，若为EDAS应用，则AppName为EDAS中的App ID，可在EDAS控制台“应用管理\>基本信息”中查看对应的ID。 |
|Namespace|String|是|default|命名空间 |
|StartTime|Long|否|1596081600000|开始时间 |
|EndTime|Long|否|1596081780000|结束时间 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|Code|String|200|返回码 |
|Data|Struct| |返回数据 |
|AppName|String|ahas-demo|应用名，若为EDAS应用，则AppName为EDAS中的App ID，可在EDAS控制台“应用管理\>基本信息”中查看对应的ID。 |
|InnerMetrics|Array of InnerMetrics| |应用监控metrics数据 |
|BlockedQps|Float|173|集群接口限流QPS |
|BlockedQpsAvg|Float|86|接口限流QPS平均值 |
|BlockedQpsMax|Float|86|接口限流QPS最大值 |
|BlockedQpsMin|Float|86|接口限流QPS最小值 |
|BlockedQpsP75|Float|86|接口限流QPS 75分位数值 |
|BlockedQpsP95|Float|86|接口限流QPS 95分位数值 |
|BlockedQpsP99|Float|86|接口限流QPS 99分位数值 |
|BlockedQpsStd|Float|0|接口限流QPS 标准差值 |
|Count|Integer|0|集群机器数 |
|Exception|Float|0|集群异常QPS |
|ExceptionAvg|Float|0|应用异常QPS平均值 |
|ExceptionMax|Float|0|应用异常QPS最大值 |
|ExceptionMin|Float|0|应用异常QPS最小值 |
|ExceptionP75|Float|0|应用异常QPS 75分位数值 |
|ExceptionP95|Float|0|应用异常QPS 95分位数值 |
|ExceptionP99|Float|0|应用异常QPS 99分位数值 |
|ExceptionStd|Float|0|应用异常QPS 标准差值 |
|PassedQps|Float|286|集群paas QPS |
|PassedQpsAvg|Float|143|应用paas QPS 平均值 |
|PassedQpsMax|Float|143|应用paas QPS 最大值 |
|PassedQpsMin|Float|143|应用paas QPS 最小值 |
|PassedQpsP75|Float|143|应用paas QPS 75分位数值 |
|PassedQpsP95|Float|143|应用paas QPS 95分位数值 |
|PassedQpsP99|Float|143|应用paas QPS 99分位数值 |
|PassedQpsStd|Float|143|应用paas QPS 标准差值 |
|Rt|Float|6.5|应用集群平均RT |
|RtAvg|Float|6.5|应用RT平均值 |
|RtMax|Float|7|应用RT最大值 |
|RtMin|Float|7|应用RT最小值 |
|RtP75|Float|7|应用RT 75分位数值 |
|RtP95|Float|7|应用RT 95分位数值 |
|RtP99|Float|7|应用RT 99分位数值 |
|RtStd|Float|0.7|应用RT 标准差值 |
|SuccessQps|Float|286|应用集群success QPS |
|SuccessQpsAvg|Float|143|应用success QPS平均值 |
|SuccessQpsMax|Float|143|应用success QPS最大值 |
|SuccessQpsMin|Float|143|应用success QPS最小值 |
|SuccessQpsP75|Float|143|应用success QPS 75分位数值 |
|SuccessQpsP95|Float|143|应用success QPS 95分位数值 |
|SuccessQpsP99|Float|143|应用success QPS 99分位数值 |
|SuccessQpsStd|Float|0|应用success QPS 标准差值 |
|Thread|Float|2|应用集群并发数 |
|ThreadAvg|Float|1|应用并发数平均值 |
|ThreadMax|Float|1|应用并发数最大值 |
|ThreadMin|Float|1|应用并发数最小值 |
|ThreadP75|Float|1|应用并发数75分位数值 |
|ThreadP95|Float|1|应用并发数95分位数值 |
|ThreadP99|Float|1|应用并发数99分位数值 |
|ThreadStd|Float|1|应用并发数标准差值 |
|Timestamp|Long|1596593014000|时间戳 |
|Namespace|String|default|命名空间 |
|Message|String|null|错误信息 |
|RequestId|String|3FEEAD12-CE22-4EDE-A729-CE94EC070610|请求ID |
|Success|Boolean|true|是否成功 |

## 示例

请求示例

```
http(s)://[Endpoint]/?Action=GetMetricsOfApp
&AppName=ahas-demo
&Namespace=default
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<GetMetricsOfAppResponse>
  <Message>null</Message>
  <RequestId>3FEEAD12-CE22-4EDE-A729-CE94EC070610</RequestId>
  <Data>
        <Namespace>default</Namespace>
        <AppName>ahas-demo</AppName>
        <InnerMetrics>
              <BlockedQps>173</BlockedQps>
              <PassedQpsMax>143</PassedQpsMax>
              <Count>0</Count>
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
              <RtMin>7</RtMin>
              <PassedQpsP95>143</PassedQpsP95>
              <ExceptionP99>0</ExceptionP99>
              <RtP75>7</RtP75>
              <ExceptionStd>0</ExceptionStd>
              <PassedQpsStd>143</PassedQpsStd>
              <SuccessQpsStd>0</SuccessQpsStd>
              <BlockedQpsMax>86</BlockedQpsMax>
              <SuccessQps>286</SuccessQps>
              <ThreadStd>1</ThreadStd>
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
</GetMetricsOfAppResponse>
```

`JSON` 格式

```
{
    "Message":"null",
"RequestId":"3FEEAD12-CE22-4EDE-A729-CE94EC070610",
    "Data":
    {
        "Namespace":"default","AppName":"ahas-demo",
        "InnerMetrics":
        [{"BlockedQps":"173",
        "PassedQpsMax":"143","Count":"0",
        "ThreadMax":"1","ThreadP75":"1",
        "SuccessQpsP75":"143","ExceptionP95":"0",
        "PassedQps":"286","RtMax":"7",
        "ThreadAvg":"1","ThreadMin":"1",
        "BlockedQpsP75":"86","BlockedQpsAvg":"86",
        "BlockedQpsMin":"86","PassedQpsP99":"143",
        "RtAvg":"6.5","RtMin":"7",
        "PassedQpsP95":"143","ExceptionP99":"0",
        "RtP75":"7","ExceptionStd":"0",
        "PassedQpsStd":"143","SuccessQpsStd":"0",
        
        "BlockedQpsMax":"86","SuccessQps":"286",
        "ThreadStd":"1","Timestamp":"1596593014000",
        "SuccessQpsP99":"143","ExceptionP75":"0",
        "ThreadP99":"1","SuccessQpsP95":"143",
        "ThreadP95":"1","RtStd":"0.7","Rt":"6.5",
        "BlockedQpsP95":"86","BlockedQpsP99":"86",
        "PassedQpsAvg":"143","PassedQpsMin":"143",
        "ExceptionAvg":"0","ExceptionMin":"0",
        "Exception":"0","SuccessQpsAvg":"143",
        "SuccessQpsMin":"143","PassedQpsP75":"143",
        "Thread":"2","RtP95":"7","RtP99":"7",
        "BlockedQpsStd":"0","ExceptionMax":"0",
        "SuccessQpsMax":"143"}]
    },
    "Code":"200",
    "Success":"true"
}
```

## 错误码

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|400|IllegalArgument.AppName|The specified AppName is invalid.|参数AppName不合法|
|400|IllegalArgument.Namespace|The specified Namespace is invalid.|参数Namespace不合法|

访问[错误中心](https://error-center.aliyun.com/status/product/ahas-openapi)查看更多错误码。

