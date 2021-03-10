---
keyword: [查看License, 公网]
---

# 查看License

License作为客户端的启动参数，用于关联客户端跟阿里云账户的关系。本文介绍如何查看License。

若用户的机器是阿里云在VPC网络环境内，且部署在杭州、上海、北京、深圳、张家口这些地域内，则无需配置License参数，默认会关联到机器所属用户下。其他情况下，用户则需要配置License参数关联到AHAS公网地域，才能使用AHAS。

## 查看License

1.  登录[AHAS控制台](https://ahas.console.aliyun.com)，在左侧导航栏选择**流量防护** \> **应用防护**。

2.  在应用防护页面右上角单击**查看License**。

    ![查看License](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/8614435161/p109733.png)


## 注意事项

-   2020年05月20日之前开通AHAS的用户，不同地域License可能不同步，若需要接入到AHAS公网，请先在[AHAS控制台](https://ahas.console.aliyun.com)页面的左上角选择公网，再查看License。

    ![切换region](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/3933858951/p109737.png)

-   License属于用户敏感信息，请勿泄露给他人使用。

