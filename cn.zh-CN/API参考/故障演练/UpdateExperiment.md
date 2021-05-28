# UpdateExperiment

调用UpdateExperiment接口编辑故障演练基本信息及流程定义。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=ahas-openapi&api=UpdateExperiment&type=RPC&version=2019-09-01)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|UpdateExperiment|系统规定参数。取值：**UpdateExperiment**。 |
|Definition|String|是|\{"runMode":"SEQUENCE","duration":600,"flowGroups":\[\{"hosts":\["192.168.0.1"\],"flows":\[\{"attack":\{"appCode":"chaos.cpu.fullload","userCheck":true,"arguments":\{"cpu\_count":"1","namespcae":"default"\}\}\}\],"appName":"demo","appGroups":\["demo-group"\]\}\]\}|故障演练流程定义。更多信息，请参见[参数说明](~~203383~~)。 |
|Name|String|是|CPU满载场景|故障演练名称 |
|Description|String|否|描述|故障演练描述 |
|NameSpace|String|是|default|演练所属的命名空间 |
|ExperimentId|String|是|1234567890123456789|故障演练ID |
|AhasRegionId|String|否|cn-hangzhou|演练所属地域ID |
|Tags.N|String|否|cn-hangzhou|地域 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|Message|String|null|错误信息 |
|RequestId|String|0f7dd92f-4490-\*\*\*\*-b8bd-\*\*\*\*|请求ID |
|HttpStatusCode|Integer|200|HTTP状态码 |
|Code|String|P\_ERROR\_\*\*\*\*|接口反馈编码 |
|Success|Boolean|true|接口请求成功标识 |

## 示例

请求示例

```
http(s)://[Endpoint]/?Action=UpdateExperiment
&ExperimentId=1234567890123456789
&Name=CPU满载场景
&NameSpace=default
&Definition={"runMode":"SEQUENCE","duration":600,"flowGroups":[{"hosts":["192.168.0.1"],"flows":[{"attack":{"appCode":"chaos.cpu.fullload","userCheck":true,"arguments":{"cpu_count":"1","namespcae":"default"}}}],"appName":"demo","appGroups":["demo-group"]}]}
&Description=描述
&Tags=["标签"]
&AhasRegionId=cn-hangzhou
&<公共请求参数>
```

正常返回示例

`XML`格式

```
HTTP/1.1 200 OK
Content-Type:application/xml

<UpdateExperimentResponse>
    <Message>null</Message>
    <RequestId>0f7dd92f-4490-****-b8bd-****</RequestId>
    <HttpStatusCode>200</HttpStatusCode>
    <Code>P_ERROR_****</Code>
    <Success>true</Success>
</UpdateExperimentResponse>
```

`JSON`格式

```
HTTP/1.1 200 OK
Content-Type:application/json

{
  "Message" : "null",
  "RequestId" : "0f7dd92f-4490-****-b8bd-****",
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

