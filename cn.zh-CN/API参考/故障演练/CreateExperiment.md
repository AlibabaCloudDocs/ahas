# CreateExperiment

调用CreateExperiment接口新建一个故障演练。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=ahas-openapi&api=CreateExperiment&type=RPC&version=2019-09-01)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|CreateExperiment|系统规定参数。取值：**CreateExperiment**。 |
|Definition|String|是|\{"runMode":"SEQUENCE","duration":600,"flowGroups":\[\{"hosts":\["192.168.0.1"\],"flows":\[\{"attack":\{"appCode":"chaos.cpu.fullload","userCheck":true,"arguments":\{"cpu\_count":"1","namespcae":"default"\}\}\}\],"appName":"demo","appGroups":\["demo-group"\]\}\]\}|演练定义。更多信息，请参见[参数说明](~~203383~~)。 |
|Name|String|是|新建演练|演练名称 |
|Description|String|否|演练描述|演练描述 |
|NameSpace|String|是|default|演练所属的命名空间 |
|AhasRegionId|String|否|cn-hangzhou|演练所属地域ID |
|Tags.N|String|否|cn-hangzhou|地域 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|0f7dd92f-4490-\*\*\*\*-b8bd-\*\*\*\*|请求ID |
|Message|String|无|接口异常信息 |
|ExperimentId|String|1234567890123456800|故障演练ID |
|HttpStatusCode|Integer|200|HTTP状态码 |
|Code|String|P\_ERROR\_\*\*\*\*|接口请求反馈编码 |
|Success|Boolean|true|接口请求成功标识 |

## 示例

请求示例

```
http(s)://[Endpoint]/?Action=CreateExperiment
&Name=新建演练
&NameSpace=default
&Definition={"runMode":"SEQUENCE","duration":600,"flowGroups":[{"hosts":["192.168.0.1"],"flows":[{"attack":{"appCode":"chaos.cpu.fullload","userCheck":true,"arguments":{"cpu_count":"1","namespcae":"default"}}}],"appName":"demo","appGroups":["demo-group"]}]}
&Description=演练描述
&Tags=["标签"]
&AhasRegionId=cn-hangzhou
&<公共请求参数>
```

正常返回示例

`XML`格式

```
HTTP/1.1 200 OK
Content-Type:application/xml

<CreateExperimentResponse>
    <RequestId>0f7dd92f-4490-****-b8bd-****</RequestId>
    <Message>无</Message>
    <ExperimentId>1234567890123456800</ExperimentId>
    <HttpStatusCode>200</HttpStatusCode>
    <Code>P_ERROR_****</Code>
    <Success>true</Success>
</CreateExperimentResponse>
```

`JSON`格式

```
HTTP/1.1 200 OK
Content-Type:application/json

{
  "RequestId" : "0f7dd92f-4490-****-b8bd-****",
  "Message" : "无",
  "ExperimentId" : "1234567890123456800",
  "HttpStatusCode" : 200,
  "Code" : "P_ERROR_****",
  "Success" : true
}
```

## 错误码

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|400|IllegalArgument|The specified parameter is invalid.|参数异常|

访问[错误中心](https://error-center.aliyun.com/status/product/ahas-openapi)查看更多错误码。

