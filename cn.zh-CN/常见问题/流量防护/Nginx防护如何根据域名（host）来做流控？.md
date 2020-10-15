# Nginx防护如何根据域名（host）来做流控？

本文介绍Nginx防护根据域名（host）做统计和流控的操作步骤。

Nginx防护在默认情况下，是按照API来进行统计和流控，如`/api/login`。Nginx大多数时候作为网关或者Proxy代理服务器转发使用，但不同的域名表示不同业务，有时需要根据不同域名来做统计和流控，可以在Nginx的HTTP配置中添加以下内容。

```
sentinel_entry $http_host
```

添加完配置之后，在[AHAS控制台](https://ahas.console.aliyun.com)的Nginx防护接口详情中会看到对不同域名的统计，可以按照API接口一样的操作进行规则配置，详情请参见[接口详情](/cn.zh-CN/应用防护/管理应用/接口详情.md)。

