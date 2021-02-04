# Nginx Sentinel模块配置

本文介绍使用Nginx接入Sentinel流量防护的配置说明。

## 安装Sentinel Sidecar

下载[AHAS Sentinel Sidecar](https://ahasoss-cn-hangzhou.oss-cn-hangzhou.aliyuncs.com/sidecar/latest/ahas-sentinel-sidecar-linux.tar.gz)，并解压到本地。

建议解压到`/opt`目录下，操作命令如下：

```
curl -L -O https://ahasoss-cn-hangzhou.oss-cn-hangzhou.aliyuncs.com/sidecar/latest/ahas-sentinel-sidecar-linux.tar.gz
sudo tar -xzf ahas-sentinel-sidecar-linux.tar.gz -C /opt/
```

解压之后的安装目录为`/opt/ahas-sentinel-sidecar-linux`，Nginx Sentinel动态模块文件位于安装目录的`lib/<os>-nginx-<version>/`子目录下。

## 全局配置

-   **加载动态模块load\_module**

    -   语法：`load_module "/path/to/module.so";`
    -   默认值： 无
    -   配置上下文：`main`
    使用Nginx Sentinel模块前，必须先使用`load_module`指令加载之。此指令必须出现在主配置文件最开始的位置（主配置`events`配置之前）。

    以CentOS 7、Nginx-1.16.1、Sentinel Sidecar安装目录`/opt/ahas-sentinel-sidecar-linux`为例，示例配置如下。

    ```
    load_module "/opt/ahas-sentinel-sidecar-linux/lib/centos7-nginx-1.16.1/ngx_sentinel_module.so";
    ```

    **说明：** Nginx 自身限制预编译动态模块与 Nginx 版本及编译配置绑定，升级 Nginx 版本或修改编译参数时必须同时更新预编译动态模块。

    如果Sentinel Sidecar安装包未包含您使用的Nginx版本，请提供您的操作系统版本和`Nginx -V`（大写的V）的完整输出文本，以便为您提供预编译Nginx模块。

-   **Nginx Sentinel模块初始化sentinel\_init**

    -   语法：`sentinel_init sidecar unix:<path> | <address>:<port>;`
    -   默认值：无
    -   配置上下文：`main`
    使用`sentinel_init`指令配置Nginx Sentinel模块初始化参数。当前即配置Sentinel Sidecar的监听地址，示例配置如下。

    ```
    sentinel_init sidecar unix:/tmp/sentinel-sidecar.sock;
    ```

-   **Sentinel Sidecar运行命令sentinel\_sidecar\_run**

    -   语法：`sentinel_sidecar_run "/path/to/sentinel-sidecar.sh" --app=<name> [--license=<license>] [--ns=<namespace>];`
    -   默认值：无
    -   配置上下文：`main`
    使用`sentinel_sidecar_run`指令配置Sentinel Sidecar运行命令。Sentinel Sidecar使用Nginx工作进程用户在独立的子进程中运行。Nginx Sentinel模块与Sidecar异步通信实现流控功能。

    在阿里云VPC环境接入时，配置如下：

    -   Sentinel Sidecar启动脚本路径，如`/opt/ahas-sentinel-sidecar-linux/bin/sentinel-sidecar.sh`。
    -   AHAS应用名`--app=<name>`。这里配置的应用名即在AHAS控制台上查看和管理的应用名。
    -   可选配置，AHAS环境（namespace）`--ns=<namespace>`。
    在公网环境接入时，还需要添加License配置：

    -   公网接入License`--license=<license>`，可登录[AHAS控制台](https://ahas.console.aliyun.com)查询您的License，详情请参见[查看License](/cn.zh-CN/流量防护/应用防护/参考信息/查看License.md)。
    **说明：** License是机密信息，请注意保密！

    以阿里云VPC环境，Sentinel Sidecar安装目录`/opt/ahas-sentinel-sidecar-linux`为例，示例配置如下。

    ```
    sentinel_sidecar_run "/opt/ahas-sentinel-sidecar-linux/bin/sentinel-sidecar.sh" --app=demo;
    ```


## HTTP限流配置

-   **限流行为sentinel\_block\_action**

    -   语法：`sentinel_block_action off | =code;`
    -   默认值：`sentinel_block_action =429;`
    -   配置上下文：`http`，`server`，`location`
    Nginx添加Sentinel模块后，可使用`sentinel_block_action`指令配置限流行为。默认配置为`sentinel_block_action =429;`，即触发限流时Nginx立即返回`HTTP 429`错误码。`sentinel_block_action`指令可分别在Nginx配置文件的http/server/location配置上下文进行配置。

    -   当客户端访问指定location下的URL请求时，如果该location未配置限流行为，则使用其所在server的配置。
    -   如果server也未配置限流行为，则使用http下的配置。
    -   如果 http下也未配置，则使用内置默认配置，即返回`HTTP 429`错误码。
    如Nginx同时作为静态资源服务器和HTTP反向代理服务器时，静态资源不需要限流，可在HTTP主配置关闭sentinel流控检查，在需要限流的location下再按需开启流控功能。

    `sentinel_block_action`指令支持如下配置项：

    -   `off`：关闭Sentinel流控检查，即不使用Sentinel模块，直接放行所有请求。
    -   `=code`：执行流控检查并执行限流拦截，触发限流时Nginx立即返回指定的HTTP错误码，拒绝处理此请求。
    **说明：** 请参考[管理API](/cn.zh-CN/流量防护/Nginx防护/管理API.md)文档将需要关注的请求URL归类为业务API，然后参考[配置流控规则](/cn.zh-CN/流量防护/Nginx防护/配置流控规则.md)文档为业务API配置流控规则。


