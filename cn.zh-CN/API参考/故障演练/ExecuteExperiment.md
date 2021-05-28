# ExecuteExperiment

调用ExecuteExperiment接口执行故障演练。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=ahas-openapi&api=ExecuteExperiment&type=RPC&version=2019-09-01)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|ExecuteExperiment|系统规定参数。取值：**ExecuteExperiment**。 |
|ExperimentId|String|是|1234567890123456789|故障演练ID |
|NameSpace|String|否|default|演练所属的命名空间 |
|Definition|String|否|\{"param":\[\{"groupId":"1234567890123456789","appName":"ahas-default-node","appGroups":\["AHAS杭州预发环境"\],"hosts":\["192.168.0.205"\],"activityParam":\[\{"flowId":"1234567890123456789","appCode":"chaos.cpu.fullload","arguments":\{"cpu\_count":"1","namespace":"default"\}\}\]\}\]\}|演练动态参数定义。更多信息，请参见[参数说明](~~203383~~)。 |
|AhasRegionId|String|否|cn-hangzhou|演练所属地域ID |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|TaskId|String|1234567890123456789|执行演练生成的演练任务实例ID |
|Message|String|无|错误信息 |
|RequestId|String|0f7dd92f-4490-\*\*\*\*-b8bd-\*\*\*\*|请求ID |
|Code|String|无|接口反馈错误编码 |
|Success|Boolean|true|接口请求成功标识 |

## 示例

请求示例

```
http(s)://[Endpoint]/?Action=ExecuteExperiment
&ExperimentId=1234567890123456789
&Definition={"param":[{"groupId":"1234567890123456789","appName":"ahas-default-node","appGroups":["AHAS杭州预发环境"],"hosts":["192.168.0.205"],"activityParam":[{"flowId":"1234567890123456789","appCode":"chaos.cpu.fullload","arguments":{"cpu_count":"1","namespace":"default"}}]}]}
&NameSpace=default
&AhasRegionId=cn-hangzhou
&<公共请求参数>
```

正常返回示例

`XML`格式

```
HTTP/1.1 200 OK
Content-Type:application/xml

<ExecuteExperimentResponse>
    <TaskId>1234567890123456789</TaskId>
    <Message>无</Message>
    <RequestId>0f7dd92f-4490-****-b8bd-****</RequestId>
    <Code>无</Code>
    <Success>true</Success>
</ExecuteExperimentResponse>
```

`JSON`格式

```
HTTP/1.1 200 OK
Content-Type:application/json

{
  "TaskId" : "1234567890123456789",
  "Message" : "无",
  "RequestId" : "0f7dd92f-4490-****-b8bd-****",
  "Code" : "无",
  "Success" : true
}
```

## 错误码

访问[错误中心](https://error-center.aliyun.com/status/product/ahas-openapi)查看更多错误码。

