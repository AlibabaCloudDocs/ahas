# FinishExperimentTask

调用FinishExperimentTask接口停止故障演练任务。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=ahas-openapi&api=FinishExperimentTask&type=RPC&version=2019-09-01)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|FinishExperimentTask|系统规定参数。取值：**FinishExperimentTask**。 |
|ExperimentTaskId|String|是|1234567890123456789|故障演练任务实例ID |
|NameSpace|String|否|default|演练所属命名空间 |
|AhasRegionId|String|否|cn-hangzhou|演练所属地域ID |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|Message|String|无|错误信息 |
|RequestId|String|0f7dd92f-4490-\*\*\*\*-b8bd-\*\*\*\*|请求ID |
|Code|String|P\_ERROR\_\*\*\*\*|接口错误编码 |
|Success|Boolean|true|接口请求成功标识 |

## 示例

请求示例

```
http(s)://[Endpoint]/?Action=FinishExperimentTask
&ExperimentTaskId=1234567890123456789
&NameSpace=default
&AhasRegionId=cn-hangzhou
&公共请求参数
```

正常返回示例

`XML`格式

```
HTTP/1.1 200 OK
Content-Type:application/xml

<FinishExperimentTaskResponse>
    <Message>无</Message>
    <RequestId>0f7dd92f-4490-****-b8bd-****</RequestId>
    <Code>P_ERROR_****</Code>
    <Success>true</Success>
</FinishExperimentTaskResponse>
```

`JSON`格式

```
HTTP/1.1 200 OK
Content-Type:application/json

{
  "Message" : "无",
  "RequestId" : "0f7dd92f-4490-****-b8bd-****",
  "Code" : "P_ERROR_****",
  "Success" : true
}
```

## 错误码

访问[错误中心](https://error-center.aliyun.com/status/product/ahas-openapi)查看更多错误码。

