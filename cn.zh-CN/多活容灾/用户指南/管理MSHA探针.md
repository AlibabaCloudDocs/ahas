---
keyword: [探针管理, 安装Agent, 卸载Agent, MSHA探针]
---

# 管理MSHA探针

安装MSHA探针可以实现多活容灾服务层和数据层的功能。本文介绍如何安装和卸载MSHA探针。

## 安装探针

1.  登录[AHAS控制台](https://ahas.console.aliyun.com)。

2.  在控制台左侧导航栏中选择**多活容灾**。

3.  在左侧导航栏选择**监控中心** \> **探针管理**。

4.  在探针管理页面，单击**查看Licence**，然后单击**复制Licences**。

5.  执行以下代码下载探针。

    ```
    wget -O ./msha-agent.jar ${地址}
    ```

    根据不同的地域设置不同的地址，具体地址信息如下：

    |地域|地址|
    |--|--|
    |杭州|http://msha-agent-hangzhou.oss-cn-hangzhou.aliyuncs.com/msha-java-agent-1.0.0.jar|
    |北京|http://msha-agent-beijing.oss-cn-beijing.aliyuncs.com/msha-java-agent-1.0.0.jar|
    |上海|http://msha-agent-shanghai.oss-cn-shanghai.aliyuncs.com/msha-java-agent-1.0.0.jar|
    |深圳|http://msha-agent-shenzhen.oss-cn-shenzhen.aliyuncs.com/msha-java-agent-1.0.0.jar|

    **说明：** 如果是EDAS应用，请使用admin账号执行。

6.  配置JVM参数。

    ```
    -javaagent:${探针安装路径}  
    -Dmsha.app.name=${应用名称} 
    -Dmsha.namespaces=${命名空间ID} 
    -Dmsha.licence=${当前license}
    ```

    **说明：**

    -   请将`${应用名称}`替换成您实际的应用名，应用名称暂不支持中文。
    -   命名空间ID之间用半角逗号（,）分隔，命名空间ID的信息可以通过命名空间概览页的**空间ID**处获取。
    -   `${当前license}`替换成您在步骤[4](#step_9ai_jal_50d)中获取到的license信息。
7.  重启应用。

    重启应用后，在探针管理页面，您的应用出现在列表中且状态显示为**在线**，则说明探针安装成功。


## 卸载探针

当您不需要使用MSHA探针时，找到需要停止的Java进程号，执行以下操作。

1.  在本地执行命令`kill -9 <进程号>`，停止应用。

2.  删除下载到本地的探针JAR包。

3.  重启应用。

    重启应用后，在探针管理页面，您的应用在列表中状态显示为**离线**，则说明探针卸载成功。


