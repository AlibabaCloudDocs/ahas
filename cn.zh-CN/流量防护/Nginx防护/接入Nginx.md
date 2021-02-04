---
keyword: [Nginx Sentinel, AHAS Sentinel Sidecar, Nginx防护]
---

# 接入Nginx

Nginx是一款高性能开源的HTTP服务器，通过Nginx Sentinel模块可以快速接入到AHAS中。当有请求流量时，您可以在Nginx防护中查看Nginx网关请求的实时QPS和RT等数据。本文介绍如何接入Nginx防护。

## 接入Nginx

1.  登录[AHAS控制台](https://ahas.console.aliyun.com)，然后在页面左上角选择**地域**。

2.  在控制台左侧导航栏中选择**流量防护** \> **Nginx防护**，然后单击**Nginx接入**。

3.  单击**接入**页签，按需选择以下任意一种方式下载AHAS Sentinel Sidecar。

    -   单击**Nginx防护**页面的**点击此处链接下载**，下载AHAS Sentinel Sidecar并用`tar`命令解压到本地。

        **说明：** 目前仅支持Linux 64位环境。

    -   执行以下命令下载并解压AHAS Sentinel Sidecar，下述命令解压之后的安装目录为/opt/ahas-sentinel-sidecar-linux。

        ```
        curl -L -O https://ahasoss-cn-hangzhou.oss-cn-hangzhou.aliyuncs.com/sidecar/latest/ahas-sentinel-sidecar-linux.tar.gz
        sudo tar -xzf ahas-sentinel-sidecar-linux.tar.gz -C /opt/
        ```

4.  添加Nginx Sentinel模块配置。

    通常可在Nginx主配置文件（默认为/etc/nginx/nginx.conf）最开头添加Sentinel模块配置。以CentOS 7，nginx-1.16.1为例，可添加配置如下。其他环境按需修改相关配置路径即可。

    -   上述第三行配置`sentinel_sidecar_run`为启动Sentinel Sidecar的命令行参数。
    -   其中`--app=${AppName}`参数配置应用名，在阿里云VPC环境下配置应用名即可自动接入AHAS控制台。
    -   如果在公网环境下测试，还需要添加`--license=<license>`参数进行公网接入认证，具体操作，请参见[查看License](/cn.zh-CN/流量防护/应用防护/参考信息/查看License.md)。

        **说明：** License是机密信息，请注意保密！

    Nginx自身限制预编译动态模块与Nginx可执行文件版本和编译配置绑定。目前默认提供以下主流GNU/Linux 64位系统和Nginx版本的预编译动态模块，位于安装目录的lib/<os\>-nginx-<version\>/子目录下。

    |操作系统|Nginx版本|动态模块路径|
    |----|-------|------|
    |Ubuntu 18.04|nginx-1.14.0|lib/ubuntu-18.04-nginx-1.14.0/ngx\_sentinel\_module.so|
    |CentOS 7|nginx-1.16.1|lib/centos7-nginx-1.16.1/ngx\_sentinel\_module.so|

    如果您使用其他Nginx版本，请您提供操作系统版本和`Nginx -V`（大写的V）的完整输出文本，以便为您提供预编译的Nginx模块。

5.  配置完成后，执行`sudo nginx -t`命令检查Nginx的配置文件和动态模块。

    除了上述核心配置外，还可以使用`sentinel_block_action`等指令控制Nginx Sentinel流控行为，详情请参见[Nginx Sentinel模块配置](/cn.zh-CN/流量防护/Nginx防护/Nginx Sentinel模块配置.md)。

6.  重启Nginx，即完成接入AHAS流量防护。

    **验证结果**

    登录[AHAS控制台](https://ahas.console.aliyun.com)，选择**流量防护** \> **Nginx防护**，在Nginx防护页面可以看到接入的Nginx，当有请求流量时，即可看到请求实时QPS和RT等统计信息。

    ![Nginx.png](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/8222119951/p141342.png)


## 体验Demo

您还可以通过Demo快速试用Nginx Sentinel流控功能。

1.  登录[AHAS控制台](https://ahas.console.aliyun.com)，然后在页面左上角选择**地域**。

2.  在控制台左侧导航栏中选择**流量防护** \> **Nginx防护**，然后单击**Nginx接入**。

3.  单击体验Demo页签，然后单击**点击此处链接下载**，下载AHAS Sentinel Sidecar并用`tar`命令解压到本地。

    **说明：** 目前仅支持Linux 64位环境。

4.  在Sentinel Sidecar安装目录的demo/子目录下，执行以下命令快速启动Demo Nginx。

    公网环境下，`xxlicensexx`请替换为您的真实License。具体操作，请参见[查看License](/cn.zh-CN/流量防护/应用防护/参考信息/查看License.md)。

    **说明：** License是机密信息，请注意保密！

    **验证结果**

    示例中Nginx默认监听8080端口，启动完成后测试访问http://localhost:8080/。登录[AHAS控制台](https://ahas.console.aliyun.com)，选择**流量防护** \> **Nginx防护**，在Nginx防护页面可以看到接入的Nginx，当有请求流量时，即可看到请求实时QPS和RT等统计信息。

5.  测试完成后，执行`./demo-nginx.sh -s quit`命令退出Demo Nginx。


## 相关文档

Nginx Sentinel详细配置文档，请参见[Nginx Sentinel模块配置](/cn.zh-CN/流量防护/Nginx防护/Nginx Sentinel模块配置.md)。



