# GetExperimentTask

调用GetExperimentTask接口查询故障演练任务详情。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=ahas-openapi&api=GetExperimentTask&type=RPC&version=2019-09-01)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|GetExperimentTask|系统规定参数。取值：**GetExperimentTask**。 |
|ExperimentTaskId|String|是|1234567890123456789|故障演练任务实例ID |
|NameSpace|String|否|default|演练所属命名空间 |
|AhasRegionId|String|否|cn-hangzhou|演练所属地域ID |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|Activities|Array of Activities| |节点场景任务详情 |
|EndTime|Long|1609430400000|节点任务结束时间 |
|StartTime|Long|1609430400000|节点任务开始时间 |
|CheckState|String|USER\_CHECK\_STATE\_PASSED|用户确认状态：

 -   USER\_CHECK\_STATE\_WAITING（等待用户确认）
-   USER\_CHECK\_STATE\_PASSED（用户确认通过）
-   USER\_CHECK\_STATE\_FAILED（用户确认失败） |
|RunResult|String|SUCCESS|节点任务执行结果：

 -   SUCCESS（成功）
-   FAILED（失败）
-   REJECTED（任务调过）
-   ERROR（任务异常中断）
-   STOPPED（任务被终止）
-   SOPPED\_FAILED（停止失败） |
|State|String|READY|节点任务状态：

 -   READY（就绪）
-   RUNNING（正在执行）
-   FINISHED（执行结束） |
|ActivityId|String|1234567890123456789|演练节点ID |
|Phase|String|ATTACK|节点所属阶段：

 -   PREPARE（准备阶段）
-   ATTACK（注入阶段）
-   CHECK（检查阶段）
-   RECOVER（恢复阶段） |
|ActivityName|String|CPU满载|演练节点任务名称 |
|ExperimentTaskId|String|1234567890123456789|故障演练任务实例ID |
|TaskId|String|1234567890123456789|节点任务实例ID |
|TaskId|String|1234567890123456789|故障演练任务实例ID |
|RequestId|String|0f7dd92f-4490-\*\*\*\*-b8bd-\*\*\*\*|请求ID |
|ExperimentName|String|测试演练|故障演练名称 |
|State|String|FINISHED|演练任务状态 |
|ExperimentId|String|1234567890123456789|故障演练任务ID |
|HttpStatusCode|Integer|200|HTTP状态码 |
|StartTime|Long|1609430400000|演练任务开始时间 |
|Success|Boolean|true|接口请求成功标识 |
|Result|String|SUCCESS|任务执行结果 |
|Namespace|String|default|命名空间 |

## 示例

请求示例

```
http(s)://[Endpoint]/?Action=GetExperimentTask
&ExperimentTaskId=1234567890123456789
&NameSpace=default
&AhasRegionId=cn-hangzhou
&<公共请求参数>
```

正常返回示例

`XML`格式

```
HTTP/1.1 200 OK
Content-Type:application/xml

<GetExperimentTaskResponse>
    <Activities>
        <EndTime>1609430400000</EndTime>
        <StartTime>1609430400000</StartTime>
        <CheckState>USER_CHECK_STATE_PASSED</CheckState>
        <RunResult>SUCCESS</RunResult>
        <State>READY</State>
        <ActivityId>1234567890123456789</ActivityId>
        <Phase>ATTACK</Phase>
        <ActivityName>CPU满载</ActivityName>
        <ExperimentTaskId>1234567890123456789</ExperimentTaskId>
        <TaskId>1234567890123456789</TaskId>
    </Activities>
    <TaskId>1234567890123456789</TaskId>
    <RequestId>0f7dd92f-4490-****-b8bd-****</RequestId>
    <ExperimentName>测试演练</ExperimentName>
    <State>FINISHED</State>
    <ExperimentId>1234567890123456789</ExperimentId>
    <HttpStatusCode>200</HttpStatusCode>
    <StartTime>1609430400000</StartTime>
    <Success>true</Success>
    <Result>SUCCESS</Result>
    <Namespace>default</Namespace>
</GetExperimentTaskResponse>
```

`JSON`格式

```
HTTP/1.1 200 OK
Content-Type:application/json

{
  "Activities" : [ {
    "EndTime" : 1609430400000,
    "StartTime" : 1609430400000,
    "CheckState" : "USER_CHECK_STATE_PASSED",
    "RunResult" : "SUCCESS",
    "State" : "READY",
    "ActivityId" : "1234567890123456789",
    "Phase" : "ATTACK",
    "ActivityName" : "CPU满载",
    "ExperimentTaskId" : "1234567890123456789",
    "TaskId" : "1234567890123456789"
  } ],
  "TaskId" : "1234567890123456789",
  "RequestId" : "0f7dd92f-4490-****-b8bd-****",
  "ExperimentName" : "测试演练",
  "State" : "FINISHED",
  "ExperimentId" : "1234567890123456789",
  "HttpStatusCode" : 200,
  "StartTime" : 1609430400000,
  "Success" : true,
  "Result" : "SUCCESS",
  "Namespace" : "default"
}
```

## 错误码

访问[错误中心](https://error-center.aliyun.com/status/product/ahas-openapi)查看更多错误码。

