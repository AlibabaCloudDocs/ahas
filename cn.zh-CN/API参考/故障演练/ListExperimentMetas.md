# ListExperimentMetas

调用ListExperimentMetas接口分页查询演练列表。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=ahas-openapi&api=ListExperimentMetas&type=RPC&version=2019-09-01)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|ListExperimentMetas|系统规定参数。取值：**ListExperimentMetas**。 |
|Page|Integer|否|1|页码（默认为1） |
|NameSpace|String|否|default|演练所属命名空间 |
|Size|Integer|否|10|分页大小（默认为10） |
|AhasRegionId|String|否|cn-hangzhou|演练所属地域ID |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|Pages|Integer|1|页码 |
|RequestId|String|0f7dd92f-4490-\*\*\*\*-b8bd-\*\*\*\*|请求ID |
|Message|String|无|错误信息 |
|PageSize|Integer|10|分页大小 |
|CurrentPage|Integer|1|当前页码 |
|Content|Array of Content| |演练列表信息 |
|State|String|READY|故障演练当前状态 |
|CreateTime|Long|1609430400000|演练创建时间 |
|ExperimentId|String|1234567890123456789|故障演练ID |
|Tags|Array of String|标签|故障演练标签 |
|Name|String|测试演练|故障演练名称 |
|Total|Integer|123|演练总数 |
|Code|String|无|接口错误编码 |
|Success|Boolean|true|接口请求成功标识 |

## 示例

请求示例

```
http(s)://[Endpoint]/?Action=ListExperimentMetas
&Page=1
&Size=10
&NameSpace=default
&AhasRegionId=cn-hangzhou
&<公共请求参数>
```

正常返回示例

`XML`格式

```
HTTP/1.1 200 OK
Content-Type:application/xml

<ListExperimentMetasResponse>
    <Pages>1</Pages>
    <RequestId>0f7dd92f-4490-****-b8bd-****</RequestId>
    <Message>无</Message>
    <PageSize>10</PageSize>
    <CurrentPage>1</CurrentPage>
    <Content>
        <State>READY</State>
        <CreateTime>1609430400000</CreateTime>
        <ExperimentId>1234567890123456789</ExperimentId>
        <Tags>标签</Tags>
        <Name>测试演练</Name>
    </Content>
    <Total>123</Total>
    <Code>无</Code>
    <Success>true</Success>
</ListExperimentMetasResponse>
```

`JSON`格式

```
HTTP/1.1 200 OK
Content-Type:application/json

{
  "Pages" : 1,
  "RequestId" : "0f7dd92f-4490-****-b8bd-****",
  "Message" : "无",
  "PageSize" : 10,
  "CurrentPage" : 1,
  "Content" : [ {
    "State" : "READY",
    "CreateTime" : 1609430400000,
    "ExperimentId" : "1234567890123456789",
    "Tags" : [ "标签" ],
    "Name" : "测试演练"
  } ],
  "Total" : 123,
  "Code" : "无",
  "Success" : true
}
```

## 错误码

访问[错误中心](https://error-center.aliyun.com/status/product/ahas-openapi)查看更多错误码。

