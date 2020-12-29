# Java SDK接入指南

您可以使用AHAS提供的Java SDK进行API调用。

## 前提条件

安装Java SDK必须用1.6或更高版本的[JDK](https://www.oracle.com/technetwork/java/javase/downloads/index.html)。

## 获取Java SDK

您可以通过Maven直接获取Java SDK（联网环境下推荐）。

打开Maven项目下的pom.xml文件，添加aliyun-java-sdk-core和aliyun-java-sdk-ahas依赖。

```
<dependency>
  <groupId>com.aliyun</groupId>
  <artifactId>aliyun-java-sdk-core</artifactId>
<version>4.5.6</version>
</dependency>
<dependency>
  <groupId>com.aliyun</groupId>
  <artifactId>aliyun-java-sdk-ahas-openapi</artifactId>
  <version>1.0.4</version>
</dependency>
```

## 使用Java SDK调用API

实际使用时，请替换以下示例中的aliyun\_user\_ak、aliyun\_user\_sk和region\_id为您实际的参数值。

```
import com.aliyuncs.DefaultAcsClient;
import com.aliyuncs.IAcsClient;
import com.aliyuncs.ahas_openapi.model.v20190901.ListFlowRulesOfAppRequest;
import com.aliyuncs.ahas_openapi.model.v20190901.ListFlowRulesOfAppResponse;
import com.aliyuncs.profile.DefaultProfile;


public class ListFlowRuleDemo {
    public static void main(String[] args){
        String regionId = "cn-hangzhou"; //执行API调用的应用所在地域ID。
        String accessKey = "**************"; //阿里云主账号或子账号的AccessKey ID。
        String accessSecret = "**************"; //阿里云主账号或子账号的AccessKey Secret。
        String appName = "ahas-demo"; //所要查询的应用名。
        String namespace = "default"; //应用所在的命名空间。

        DefaultProfile profile = DefaultProfile.getProfile(regionId, accessKey, accessSecret);
        IAcsClient client = new DefaultAcsClient(profile);
        ListFlowRulesOfAppRequest request = new ListFlowRulesOfAppRequest();
        //公网调用openAPI需要额外设置ahasRegionId=public，其他region请勿设置！！！
        request.setAhasRegionId("public");
        request.setAppName(appName);
        request.setNamespace(namespace);
        try{
            //发送请求
            ListFlowRulesOfAppResponse response = client.getAcsResponse(request);
            //获取并处理返回结果
            System.out.println(response.getData());
        }catch(Exception e){
            e.printStackTrace();
        }
    }
}
```

## 地域和接入点列表

AHAS API的服务接入地址。不同地域的接入地址如下表所示。

|地域名称|RegionId|Endpoint|
|----|--------|--------|
|华东1（杭州）|cn-hangzhou|ahas.cn-hangzhou.aliyuncs.com|
|华东2（上海）|cn-shanghai|ahas.cn-shanghai.aliyuncs.com|
|华北2（北京）|cn-beijing|ahas.cn-beijing.aliyuncs.com|
|华北3（张家口）|cn-zhangjiakou|ahas.cn-zhangjiakou.aliyuncs.com|
|华南1（深圳）|cn-shenzhen|ahas.cn-shenzhen.aliyuncs.com|
|公网|cn-hangzhou|ahas.cn-hangzhou.aliyuncs.com|

