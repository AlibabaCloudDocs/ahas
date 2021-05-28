# GetActivityTask

调用GetActivityTask接口查询节点任务详情。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=ahas-openapi&api=GetActivityTask&type=RPC&version=2019-09-01)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|GetActivityTask|系统规定参数。取值：**GetActivityTask**。 |
|ExperimentTaskId|String|是|1234567890123456789|故障演练任务实例ID |
|NameSpace|String|否|default|演练所属命名空间 |
|ActivityTaskId|String|是|1234567890123456789|节点任务实例ID |
|AhasRegionId|String|否|cn-hangzhou|演练所属地域ID |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|Hosts|Array of Hosts| |机器执行信息 |
|HostIp|String|192.168.0.1|节点机器IP |
|EndTime|Long|1609430400000|节点机器任务结束时间 |
|StartTime|Long|1609430400000|节点机器任务开始时间 |
|Data|String|无|小程序返回值，页面以Pretty JSON String形式展示 |
|ErrorMessage|String|无|节点机器执行错误信息 |
|ExpId|String|3456\*\*\*\*|节点机器任务执行ID |
|Result|String|SUCCESS|节点机器任务执行结果 |
|State|String|FINISHED|节点机器任务状态 |
|TaskId|String|1234567890123456789|节点任务实例ID |
|Phase|String|ATTACK|节点所属阶段：

 -   PREPARE（准备阶段）
-   ATTACK（注入阶段）
-   CHECK（检查阶段）
-   RECOVER（恢复阶段） |
|EndTime|Long|1609430400000|节点任务结束时间 |
|RequestId|String|0f7dd92f-4490-\*\*\*\*-b8bd-\*\*\*\*|请求ID |
|ActivityName|String|CPU满载|节点任务实例名称 |
|State|String|FINISHED|节点任务状态：

 -   READY（就绪）
-   RUNNING（正在执行）
-   FINISHED（执行结束） |
|ActivityId|String|1234567890123456789|节点任务实例ID |
|ExperimentTaskId|String|1234567890123456789|故障演练任务实例ID |
|HttpStatusCode|Integer|200|HTTP状态码 |
|StartTime|Long|1609430400000|节点任务开始时间 |
|RunResult|String|SUCCESS|节点任务执行结果：

 -   SUCCESS（成功）
-   FAILED（失败）
-   REJECTED（任务调过）
-   ERROR（任务异常中断）
-   STOPPED（任务被终止）
-   SOPPED\_FAILED（停止失败） |
|Success|Boolean|true|接口请求成功标识 |

## 示例

请求示例

```
http(s)://[Endpoint]/?Action=GetActivityTask
&ActivityTaskId=1234567890123456789
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

<GetActivityTaskResponse>
    <Hosts>
        <HostIp>192.168.0.1</HostIp>
        <EndTime>1609430400000</EndTime>
        <StartTime>1609430400000</StartTime>
        <Data>无</Data>
        <ErrorMessage>无</ErrorMessage>
        <ExpId>3456****</ExpId>
        <Result>SUCCESS</Result>
        <State>FINISHED</State>
        <TaskId>1234567890123456789</TaskId>
    </Hosts>
    <Phase>ATTACK</Phase>
    <EndTime>1609430400000</EndTime>
    <RequestId>0f7dd92f-4490-****-b8bd-****</RequestId>
    <ActivityName>CPU满载</ActivityName>
    <State>FINISHED</State>
    <ActivityId>1234567890123456789</ActivityId>
    <ExperimentTaskId>1234567890123456789</ExperimentTaskId>
    <HttpStatusCode>200</HttpStatusCode>
    <StartTime>1609430400000</StartTime>
    <RunResult>SUCCESS</RunResult>
    <Success>true</Success>
</GetActivityTaskResponse>
```

`JSON`格式

```
HTTP/1.1 200 OK
Content-Type:application/json

{
  "Hosts" : [ {
    "HostIp" : "192.168.0.1",
    "EndTime" : 1609430400000,
    "StartTime" : 1609430400000,
    "Data" : "无",
    "ErrorMessage" : "无",
    "ExpId" : "3456****",
    "Result" : "SUCCESS",
    "State" : "FINISHED",
    "TaskId" : "1234567890123456789"
  } ],
  "Phase" : "ATTACK",
  "EndTime" : 1609430400000,
  "RequestId" : "0f7dd92f-4490-****-b8bd-****",
  "ActivityName" : "CPU满载",
  "State" : "FINISHED",
  "ActivityId" : "1234567890123456789",
  "ExperimentTaskId" : "1234567890123456789",
  "HttpStatusCode" : 200,
  "StartTime" : 1609430400000,
  "RunResult" : "SUCCESS",
  "Success" : true
}
```

## 错误码

访问[错误中心](https://error-center.aliyun.com/status/product/ahas-openapi)查看更多错误码。

