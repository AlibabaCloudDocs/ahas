# PageableQueryUserExperiment

调用PageableQueryUserExperiment接口查询用户演练列表。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=ahas-openapi&api=PageableQueryUserExperiment&type=RPC&version=2019-09-01)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|PageableQueryUserExperiment|系统规定参数。取值：**PageableQueryUserExperiment**。 |
|SearchKey|String|否|演练名称检索|演练检索关键字 |
|State|String|否|READY|演练状态 |
|Page|Integer|否|1|页码 |
|Size|Integer|否|10|分页大小 |
|Namespace|String|否|default|演练所属的命名空间 |
|AhasRegionId|String|否|cn-public|演练所属地域ID（调用公网接口使用） |
|WorkspaceId|String|否|1234567890123456789|演练空间ID。若传入该字段则查询指定空间的演练列表，否则查询用户默认空间的演练列表。 |
|RegionId|String|否|cn-hangzhou|地域。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|Pages|Integer|2|页数 |
|RequestId|String|0f7dd92f-4490-\*\*\*\*-b8bd-\*\*\*\*|请求ID |
|Message|String|null|接口异常信息 |
|PageSize|Integer|10|每页数据条数 |
|CurrentPage|Integer|1|当前页码 |
|Total|Integer|20|数据总数 |
|ExperimentList|Array of ExperimentInfo| |演练列表 |
|Permission|Integer|7|当前账号对故障演练权限：

 -   1：只读权限
-   2：编辑权限
-   4：执行权限
-   7：所有权限 |
|Result|String|SUCCESS|故障演练最后一次任务的执行结果：

 -   SUCCESS（成功）
-   FAILED（失败）
-   REJECTED（任务调过）
-   ERROR（任务异常中断）
-   STOPPED（任务被终止）
-   SOPPED\_FAILED（停止失败） |
|State|String|READY|演练状态：

 -   READY（就绪）
-   RUNNING（正在执行）
-   FINISHED（执行结束） |
|CreateTime|Long|1611835037000|演练创建时间 |
|ExperimentId|String|1234567890123456789|故障演练ID |
|Tags|Array of String|演练标签|故障演练标签 |
|MiniApps|Array of String|cpu|故障演练有关的小程序 |
|Name|String|演练名称|故障演练名称 |
|Creator|String|1XXXXXXXXXX|演练创建人UserID |
|HttpStatusCode|Integer|200|HTTP状态码 |
|Code|String|P\_ERROR\_\*\*\*\*|接口请求反馈编码 |
|Success|Boolean|true|接口请求成功标识 |

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
&WorkspaceId=1234567890123456789
&<公共请求参数>
```

正常返回示例

`XML`格式

```
HTTP/1.1 200 OK
Content-Type:application/xml

<PageableQueryUserExperimentResponse>
    <Pages>2</Pages>
    <RequestId>0f7dd92f-4490-****-b8bd-****</RequestId>
    <Message>null</Message>
    <PageSize>10</PageSize>
    <CurrentPage>1</CurrentPage>
    <Total>20</Total>
    <ExperimentList>
        <Permission>7</Permission>
        <Result>SUCCESS</Result>
        <State>READY</State>
        <CreateTime>1611835037000</CreateTime>
        <ExperimentId>1234567890123456789</ExperimentId>
        <Tags>演练标签</Tags>
        <MiniApps>cpu</MiniApps>
        <Name>演练名称</Name>
        <Creator>1XXXXXXXXXX</Creator>
    </ExperimentList>
    <HttpStatusCode>200</HttpStatusCode>
    <Code>P_ERROR_****</Code>
    <Success>true</Success>
</PageableQueryUserExperimentResponse>
```

`JSON`格式

```
HTTP/1.1 200 OK
Content-Type:application/json

{
  "Pages" : 2,
  "RequestId" : "0f7dd92f-4490-****-b8bd-****",
  "Message" : "null",
  "PageSize" : 10,
  "CurrentPage" : 1,
  "Total" : 20,
  "ExperimentList" : [ {
    "Permission" : 7,
    "Result" : "SUCCESS",
    "State" : "READY",
    "CreateTime" : 1611835037000,
    "ExperimentId" : "1234567890123456789",
    "Tags" : [ "演练标签" ],
    "MiniApps" : [ "cpu" ],
    "Name" : "演练名称",
    "Creator" : "1XXXXXXXXXX"
  } ],
  "HttpStatusCode" : 200,
  "Code" : "P_ERROR_****",
  "Success" : true
}
```

## 错误码

访问[错误中心](https://error-center.aliyun.com/status/product/ahas-openapi)查看更多错误码。

