# PageableQueryExperimentTaskByExperimentId

调用PageableQueryExperimentTaskByExperimentId接口根据演练ID分页查询演练任务。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=ahas-openapi&api=PageableQueryExperimentTaskByExperimentId&type=RPC&version=2019-09-01)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|PageableQueryExperimentTaskByExperimentId|系统规定参数。取值：PageableQueryExperimentTaskByExperimentId。 |
|ExperimentId|String|否|1234567890123456789|故障演练ID |
|Page|Integer|否|1|页码 |
|Size|Integer|否|10|分页大小 |
|Namespace|String|否|default|命名空间 |
|RegionId|String|否|cn-hangzhou|演练所属地域ID |
|AhasRegionId|String|否|cn-public|演练所属地域ID（调用公网环境时使用） |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|Code|String|P\_ERROR\_\*\*\*\*|接口请求反馈编码 |
|CurrentPage|Integer|1|当前页码 |
|ExperimentTasks|Array of ExperimentTaskInfo| |演练任务信息 |
|Creator|Struct| |创建人（执行人） |
|SubUserId|String|2XXXXXXXXXXXXX|RAM用户ID（主账号操作，该字段为空） |
|UserId|String|1XXXXXXXXXXXXX|阿里云账号ID |
|CurrentPhase|String|null|当前执行阶段（运行中的任务属性） |
|EndTime|Long|1611835105000|演练任务结束时间 |
|ExperimentId|String|1234567890123456789|故障演练ID |
|ExperimentName|String|故障演练|故障演练名称 |
|ExtInfo|Struct| |演练其他信息 |
|SchedulerConfig|Struct| |演练定时执行信息 |
|CronExpression|String|0 0 1 \* \* ? \*|定时任务表达式 |
|FixedTime|String|1611835105000|指定一次时间执行 |
|Message|String|null|任务执行错误信息 |
|Result|String|SUCCESS|任务执行结果 |
|StartTime|Long|1611835037000|演练任务开始时间 |
|State|String|FINISHED|演练任务状态 |
|TaskId|String|1234567890123456789|演练任务ID |
|HttpStatusCode|Integer|200|HTTP状态码 |
|Message|String|null|接口异常信息 |
|PageSize|Integer|10|每页大小 |
|Pages|Integer|2|总页数 |
|RequestId|String|0f7dd92f-4490-\*\*\*\*-b8bd-\*\*\*\*|请求ID |
|Success|Boolean|true|接口请求成功标识 |
|Total|Integer|20|总数据数 |

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
<PageableQueryExperimentTaskByExperimentId>
  <Pages>2</Pages>
  <ExperimentTasks>
        <CurrentPhase>null</CurrentPhase>
        <TaskId>1234567890123456789</TaskId>
        <Message>null</Message>
        <EndTime>1611835105000</EndTime>
        <ExperimentName>故障演练</ExperimentName>
        <State>FINISHED</State>
        <ExperimentId>1234567890123456789</ExperimentId>
        <StartTime>1611835037000</StartTime>
        <Result>SUCCESS</Result>
        <ExtInfo>
              <SchedulerConfig>
                    <CronExpression>0 0 1 * * ? *</CronExpression>
                    <FixedTime>1611835105000</FixedTime>
              </SchedulerConfig>
        </ExtInfo>
        <Creator>
              <UserId>1XXXXXXXXXXXXX</UserId>
              <SubUserId>2XXXXXXXXXXXXX</SubUserId>
        </Creator>
  </ExperimentTasks>
  <PageSize>10</PageSize>
  <RequestId>0f7dd92f-4490-****-b8bd-****</RequestId>
  <Message>null</Message>
  <CurrentPage>1</CurrentPage>
  <Total>20</Total>
  <HttpStatusCode>200</HttpStatusCode>
  <Code>P_ERROR_****</Code>
  <Success>true</Success>
</PageableQueryExperimentTaskByExperimentId>
```

`JSON`格式

```
{
    "Pages":"2",
    "ExperimentTasks":[
        {
            "CurrentPhase":"null",
            "TaskId":"1234567890123456789",
            "Message":"null",
            "EndTime":"1611835105000",
            "ExperimentName":"故障演练",
            "State":"FINISHED",
            "ExperimentId":"1234567890123456789",
            "StartTime":"1611835037000",
            "Result":"SUCCESS",
            "ExtInfo":{
                "SchedulerConfig":{
                    "CronExpression":"0 0 1 * * ? *",
                    "FixedTime":"1611835105000"
                }
            },
            "Creator":{
                "UserId":"1XXXXXXXXXXXXX",
                "SubUserId":"2XXXXXXXXXXXXX"
            }
        }
    ],
    "PageSize":"10",
    "RequestId":"0f7dd92f-4490-****-b8bd-****",
    "Message":"null",
    "CurrentPage":"1",
    "Total":"20",
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

