---
keyword: [Http Client, OkHttp, 流量防护]
---

# 接入Http Client

AHAS的流量防护支持接入Http Client，首先应用通过SDK方式接入，然后将应用中的Http Client调用再接入AHAS控制台，使Http Client可以使用流量防护服务。目前AHAS提供OkHttp及Apache HttpClient（同步模式）框架的适配。本文介绍如何接入Http Client。

-   已通过SDK方式在AHAS应用防护中接入应用，具体操作，请参见[接入应用方式](/cn.zh-CN/流量防护/应用防护/接入应用/接入应用方式.md)。
-   如果您要接入的应用是Spring Boot/Spring Cloud，具体操作，请参见[接入Spring Boot/Spring Cloud应用](/cn.zh-CN/流量防护/应用防护/接入应用/接入JAVA SDK应用/接入Spring Boot/Spring Cloud应用.md)。

## 接入OkHttp

若要将OkHttp接入AHAS流量防护，您只需在创建OkHttpClient的时候通过以下方式注册AHAS Sentinel的Interceptor：

```
OkHttpClient client = new OkHttpClient.Builder()
        .addInterceptor(new SentinelOkHttpInterceptor(new SentinelOkHttpConfig()))
        .build();
```

**说明：** AHAS默认会提取Http Method与URL以`okhttp:${httpMethod}:${url}`的模式拼接作为资源名，如`okhttp:GET:http://localhost:8088/hello`。

您也可以在创建`SentinelOkHttpInterceptor`时在`SentinelOkHttpConfig`中自定义解析资源名的逻辑（`OkHttpResourceExtractor`），示例如下：

```
OkHttpResourceExtractor extractor = (request, connection) -> {
    String resource = request.url().toString();
    String regex = "/okhttp/back/";
    if (resource.contains(regex)) {
        resource = resource.substring(0, resource.indexOf(regex) + regex.length()) + "{id}";
    }
    return resource;
};
```

默认情况下URL访问被限流后会抛出`RuntimeException("SentinelBlockException")`异常。您也可以在创建`SentinelOkHttpConfig`时提供自定义的Fallback处理器。Fallback示例如下：

```
public class SomeFallback implements OkHttpFallback {

    @Override
    public Response handle(Request request, Connection connection, BlockException e) {
        //在此处构造限流后的response。
        return new Response(myErrorBuilder);
    }
}
```

## 接入Apache HttpClient

**说明：** 目前仅支持同步模式的CloseableHttpClient。

若要将Apache HttpClient接入AHAS流量防护，您只需通过以下方式使用`SentinelApacheHttpClientBuilder`构造`CloseableHttpClient`：

```
HttpClientBuilder builder = new SentinelApacheHttpClientBuilder(config); //使用方式同正常的builder，可以传入自定义的配置。
CloseableHttpClient httpClient = builder.build();
```

`SentinelApacheHttpClientBuilder`的使用方式和正常的`HttpClientBuilder`相同，可以传入自定义的Http Client配置。AHAS默认会提取Http Method与URL以`httpclient:${httpMethod}:${url}`的模式拼接作为资源名，如 `httpclient:GET:http://localhost:8088/hello`。

您也可以在创建`SentinelApacheHttpClientBuilder`时在`SentinelApacheHttpClientConfig`中自定义解析资源名的逻辑 （extractor）。

默认情况下URL访问被限流后会抛出`RuntimeException("SentinelBlockException")`异常。您也可以在创建`SentinelApacheHttpClientConfig`时提供自定义的Fallback处理器。Fallback示例如下：

```
public class MyApacheHttpClientFallback implements ApacheHttpClientFallback {

    @Override
    public CloseableHttpResponse handle(HttpRequestWrapper request, BlockException e) {
        //在此处构造限流后的response。
    }
}
```

## 相关文档

关于AHAS应用防护接入的相关文档如下：

-   [接入Spring Boot/Spring Cloud应用](/cn.zh-CN/流量防护/应用防护/接入应用/接入JAVA SDK应用/接入Spring Boot/Spring Cloud应用.md)
-   [接入Spring应用](/cn.zh-CN/流量防护/应用防护/接入应用/接入JAVA SDK应用/接入Spring应用.md)
-   [接入Dubbo应用](/cn.zh-CN/流量防护/应用防护/接入应用/接入JAVA SDK应用/接入Dubbo应用.md)
-   [接入HSF应用](/cn.zh-CN/流量防护/应用防护/接入应用/接入JAVA SDK应用/接入HSF应用.md)
-   [接入Web应用](/cn.zh-CN/流量防护/应用防护/接入应用/接入JAVA SDK应用/接入Web应用.md)
-   [通过自定义埋点接入](/cn.zh-CN/流量防护/应用防护/接入应用/接入JAVA SDK应用/通过自定义埋点接入.md)
-   [接入MyBatis应用](/cn.zh-CN/流量防护/应用防护/接入应用/接入JAVA SDK应用/接入MyBatis应用.md)

