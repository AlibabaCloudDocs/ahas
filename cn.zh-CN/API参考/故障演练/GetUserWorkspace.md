# GetUserWorkspace

调用GetUserWorkspace接口查询用户下所有演练空间，包括默认空间、管理空间和参与空间。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=ahas-openapi&api=GetUserWorkspace&type=RPC&version=2019-09-01)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|GetUserWorkspace|系统规定参数。取值：GetUserWorkspace。 |
|Namespace|String|否|default|演练所属的命名空间 |
|AhasRegionId|String|否|cn-hangzhou|演练所属地域ID |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|0f7dd92f-4490-xxxx-b8bd-xxxxxxxxxxxxx|RequestID |
|HttpStatusCode|Integer|200|HTTP状态码 |
|Code|String|P\_ERROR\_XXXXXXX|接口错误编码 |
|Message|String|null|错误信息 |
|Success|Boolean|true|接口请求成功标识 |
|WorkspaceList|Array of WorkspaceInfo| |演练空间信息列表 |
|Description|String|演练空间描述|演练空间描述 |
|Name|String|演练空间名称|演练空间名称 |
|Type|Integer|0|演练空间类型：

 -   0：默认空间
-   1：用户空间 |
|WorkspaceId|String|1234567890123456789|演练空间ID |

## 示例

请求示例

```
http(s)://[Endpoint]/?Action=GetUserWorkspace
&Namespace=default
&AhasRegionId=cn-hangzhou
&<公共请求参数>
```

正常返回示例

`XML`格式

```
<GetUserWorkspace>
  <RequestId>0f7dd92f-4490-xxxx-b8bd-xxxxxxxxxxxxx</RequestId>
  <Message>null</Message>
  <HttpStatusCode>200</HttpStatusCode>
  <WorkspaceList>
        <Type>0</Type>
        <Description>演练空间描述</Description>
        <WorkspaceId>1234567890123456789</WorkspaceId>
        <Name>演练空间名称</Name>
  </WorkspaceList>
  <Code>P_ERROR_XXXXXXX</Code>
  <Success>true</Success>
</GetUserWorkspace>
```

`JSON`格式

```
{
    "RequestId":"0f7dd92f-4490-xxxx-b8bd-xxxxxxxxxxxxx",
    "Message":"null",
    "HttpStatusCode":"200",
    "WorkspaceList":[
        {
            "Type":"0",
            "Description":"演练空间描述",
            "WorkspaceId":"1234567890123456789",
            "Name":"演练空间名称"
        }
    ],
    "Code":"P_ERROR_XXXXXXX",
    "Success":"true"
}
```

## 错误码

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|400|IllegalArgument|The specified parameter is invalid.|参数异常|

访问[错误中心](https://error-center.aliyun.com/status/product/ahas-openapi)查看更多错误码。

