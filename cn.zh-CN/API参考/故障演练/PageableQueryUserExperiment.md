# PageableQueryUserExperiment

调用PageableQueryUserExperiment接口查询用户演练列表。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=ahas-openapi&api=PageableQueryUserExperiment&type=RPC&version=2019-09-01)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|PageableQueryUserExperiment|系统规定参数。取值：PageableQueryUserExperiment。 |
|SearchKey|String|否|演练检索关键字|演练检索关键字 |
|State|String|否|READY|演练状态 |
|Page|Integer|否|1|页码 |
|Size|Integer|否|10|分页大小 |
|Namespace|String|否|default|演练所属的命名空间 |
|RegionId|String|否|cn-hangzhou|地域 |
|AhasRegionId|String|否|cn-public|演练所属地域ID（调用公网接口使用） |
|Tags.N|RepeatList|否|演练标签|演练检索标签 |
|Results.N|RepeatList|否|FINISHED|演练最后一次任务运行结果 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|Code|String|P\_ERROR\_\*\*\*\*|接口请求反馈编码 |
|CurrentPage|Integer|1|当前页码 |
|ExperimentList|Array of ExperimentInfo| |演练列表 |
|CreateTime|Long|1611835037000|演练创建时间 |
|Creator|String|1XXXXXXXXXX|演练创建人UserID |
|ExperimentId|String|1234567890123456789|故障演练ID |
|MiniApps|List|cpu|故障演练有关的小程序 |
|Name|String|演练名称|故障演练名称 |
|Permission|Integer|7|当前账号对故障演练权限 |
|Result|String|SUCCESS|故障演练最后一次任务的执行结果 |
|State|String|READY|演练状态 |
|Tags|List|演练标签|故障演练标签 |
|HttpStatusCode|Integer|200|HTTP状态码 |
|Message|String|null|接口异常信息 |
|PageSize|Integer|10|每页数据条数 |
|Pages|Integer|2|页数 |
|RequestId|String|0f7dd92f-4490-\*\*\*\*-b8bd-\*\*\*\*|请求ID |
|Success|Boolean|true|接口请求成功标识 |
|Total|Integer|20|数据总数 |

## 示例

请求示例

```
http(s)://[Endpoint]/?Action=PageableQueryUserExperiment
&SearchKey=演练名称检索
&State=READY
&Page=1
&Size=10
&Namespace=default
&RegionId=cn-hangzhou
&AhasRegionId=cn-public
&Tags.N=演练标签
&Results.N=FINISHED
&<公共请求参数>
```

正常返回示例

`XML`格式

```
<PageableQueryUserExperiment>
  <Pages>2</Pages>
  <PageSize>10</PageSize>
  <RequestId>0f7dd92f-4490-****-b8bd-****</RequestId>
  <Message>null</Message>
  <CurrentPage>1</CurrentPage>
  <Total>20</Total>
  <ExperimentList>
        <State>READY</State>
        <ExperimentId>1234567890123456789</ExperimentId>
        <CreateTime>1611835037000</CreateTime>
        <Permission>7</Permission>
        <Creator>1XXXXXXXXXX</Creator>
        <Result>SUCCESS</Result>
        <Name>演练名称</Name>
        <Tags>演练标签</Tags>
        <MiniApps>cpu</MiniApps>
  </ExperimentList>
  <HttpStatusCode>200</HttpStatusCode>
  <Code>P_ERROR_****</Code>
  <Success>true</Success>
</PageableQueryUserExperiment>
```

`JSON`格式

```
{
    "Pages":"2",
    "PageSize":"10",
    "RequestId":"0f7dd92f-4490-****-b8bd-****",
    "Message":"null",
    "CurrentPage":"1",
    "Total":"20",
    "ExperimentList":[
        {
            "State":"READY",
            "ExperimentId":"1234567890123456789",
            "CreateTime":"1611835037000",
            "Permission":"7",
            "Creator":"1XXXXXXXXXX",
            "Result":"SUCCESS",
            "Name":"演练名称",
            "Tags":"演练标签",
            "MiniApps":"cpu"
        }
    ],
    "HttpStatusCode":"200",
    "Code":"P_ERROR_****",
    "Success":"true"
}
```

## 错误码

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|400|IllegalArgument|The specified parameter is invalid.|参数异常|

访问[错误中心](https://error-center.aliyun.com/status/product/ahas-openapi)查看更多错误码。

