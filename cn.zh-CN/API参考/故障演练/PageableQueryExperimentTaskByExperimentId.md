# PageableQueryExperimentTaskByExperimentId

调用PageableQueryExperimentTaskByExperimentId接口根据演练ID分页查询演练任务。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=ahas-openapi&api=PageableQueryExperimentTaskByExperimentId&type=RPC&version=2019-09-01)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|PageableQueryExperimentTaskByExperimentId|系统规定参数。取值：**PageableQueryExperimentTaskByExperimentId**。 |
|ExperimentId|String|否|1234567890123456789|故障演练ID |
|Page|Integer|否|1|页码 |
|Size|Integer|否|10|分页大小 |
|Namespace|String|否|default|命名空间 |
|RegionId|String|否|cn-hangzhou|演练所属地域ID |
|AhasRegionId|String|否|cn-public|演练所属地域ID（调用公网环境时使用） |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|Pages|Integer|2|总页数 |
|ExperimentTasks|Array of ExperimentTaskInfo| |演练任务信息 |
|EndTime|Long|1611835105000|演练任务结束时间 |
|StartTime|Long|1611835037000|演练任务开始时间 |
|Result|String|SUCCESS|任务执行结果 |
|State|String|FINISHED|演练任务状态 |
|CurrentPhase|String|null|当前执行阶段（运行中的任务属性） |
|ExperimentId|String|1234567890123456789|故障演练ID |
|Message|String|null|任务执行错误信息 |
|TaskId|String|1234567890123456789|演练任务ID |
|ExperimentName|String|故障演练|故障演练名称 |
|ExtInfo|Object| |演练其他信息 |
|SchedulerConfig|Object| |演练定时执行信息 |
|FixedTime|String|1611835105000|指定一次时间执行 |
|CronExpression|String|0 0 1 \* \* ? \*|定时任务表达式 |
|Creator|Object| |创建人（执行人） |
|SubUserId|String|2XXXXXXXXXXXXX|RAM用户ID（主账号操作，该字段为空） |
|UserId|String|1XXXXXXXXXXXXX|阿里云账号ID |
|Namespace|String|default|命名空间 |
|RequestId|String|0f7dd92f-4490-\*\*\*\*-b8bd-\*\*\*\*|请求ID |
|Message|String|null|接口异常信息 |
|PageSize|Integer|10|每页大小 |
|CurrentPage|Integer|1|当前页码 |
|Total|Integer|20|总数据数 |
|HttpStatusCode|Integer|200|HTTP状态码 |
|Code|String|P\_ERROR\_\*\*\*\*|接口请求反馈编码 |
|Success|Boolean|true|接口请求成功标识 |

## 示例

请求示例

```
http(s)://[Endpoint]/?Action=PageableQueryExperimentTaskByExperimentId
&ExperimentId=1234567890123456789
&Page=1
&Size=10
&Namespace=default
&RegionId=cn-hangzhou
&AhasRegionId=cn-public
&<公共请求参数>
```

正常返回示例

`XML`格式

```
HTTP/1.1 200 OK
Content-Type:application/xml

<PageableQueryExperimentTaskByExperimentIdResponse>
    <Pages>2</Pages>
    <ExperimentTasks>
        <EndTime>1611835105000</EndTime>
        <StartTime>1611835037000</StartTime>
        <Result>SUCCESS</Result>
        <State>FINISHED</State>
        <CurrentPhase>null</CurrentPhase>
        <ExperimentId>1234567890123456789</ExperimentId>
        <Message>null</Message>
        <TaskId>1234567890123456789</TaskId>
        <ExperimentName>故障演练</ExperimentName>
        <ExtInfo>
            <SchedulerConfig>
                <FixedTime>1611835105000</FixedTime>
                <CronExpression>0 0 1 * * ? *</CronExpression>
            </SchedulerConfig>
        </ExtInfo>
        <Creator>
            <SubUserId>2XXXXXXXXXXXXX</SubUserId>
            <UserId>1XXXXXXXXXXXXX</UserId>
        </Creator>
        <Namespace>default</Namespace>
    </ExperimentTasks>
    <RequestId>0f7dd92f-4490-****-b8bd-****</RequestId>
    <Message>null</Message>
    <PageSize>10</PageSize>
    <CurrentPage>1</CurrentPage>
    <Total>20</Total>
    <HttpStatusCode>200</HttpStatusCode>
    <Code>P_ERROR_****</Code>
    <Success>true</Success>
</PageableQueryExperimentTaskByExperimentIdResponse>
```

`JSON`格式

```
HTTP/1.1 200 OK
Content-Type:application/json

{
  "Pages" : 2,
  "ExperimentTasks" : [ {
    "EndTime" : 1611835105000,
    "StartTime" : 1611835037000,
    "Result" : "SUCCESS",
    "State" : "FINISHED",
    "CurrentPhase" : "null",
    "ExperimentId" : "1234567890123456789",
    "Message" : "null",
    "TaskId" : "1234567890123456789",
    "ExperimentName" : "故障演练",
    "ExtInfo" : {
      "SchedulerConfig" : {
        "FixedTime" : "1611835105000",
        "CronExpression" : "0 0 1 * * ? *"
      }
    },
    "Creator" : {
      "SubUserId" : "2XXXXXXXXXXXXX",
      "UserId" : "1XXXXXXXXXXXXX"
    },
    "Namespace" : "default"
  } ],
  "RequestId" : "0f7dd92f-4490-****-b8bd-****",
  "Message" : "null",
  "PageSize" : 10,
  "CurrentPage" : 1,
  "Total" : 20,
  "HttpStatusCode" : 200,
  "Code" : "P_ERROR_****",
  "Success" : true
}
```

## 错误码

访问[错误中心](https://error-center.aliyun.com/status/product/ahas-openapi)查看更多错误码。

