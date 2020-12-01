---
keyword: [PHP应用, SDK接入, 应用防护]
---

# 接入PHP应用

将PHP应用接入AHAS应用防护后，可以对其配置流控、降级、隔离和系统规则来保证系统稳定性。本文介绍如何使用SDK方式将PHP应用接入应用防护。

目前仅支持Linux 64位环境，请确保您的PHP版本≥7.0或者≥5.5并通过composer管理依赖。

## PHP应用接入步骤

1.  登录[AHAS控制台](https://ahas.console.aliyun.com)，然后在页面左上角选择**地域**。

2.  在控制台左侧导航栏中选择**流量防护** \> **应用防护**。

3.  在应用防护页面右上角单击**新应用接入**，然后单击**PHP语言**，选择**SDK接入**。

4.  在**自定义埋点**单击**下载AHAS Sentinel Sidecar**，然后将压缩包解压到本地。

5.  进入压缩包解压后的路径，然后执行以下命令启动Sentinel Sidecar。



    若在公网地域，需要查看License信息。请在**PHP语言**页签查看（非公网地域不需要），具体请参见[查看License](/cn.zh-CN/流量防护/应用防护/参考信息/查看License.md)。

    ![PHP license.png](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/1733858951/p139655.png)

    停止应用后，可执行以下命令退出Sentinel Sidecar：

    ```
    ./bin/sentinel-sidecar.sh --quit
    ```

6.  在您的PHP项目中添加AHAS Sentinel依赖。

    ```
    composer require ahas/sentinel "^0"
    ```

    **说明：** 通常需要在PHP源码文件头部引入composer autoload文件，以支持自动加载PHP类。

7.  在代码中创建SentinelClient实例。

    ```
    // 创建AHAS Sentinel客户端，本地sidecar默认监听9090端口。
    sentinel = new \Sentinel\SentinelClient("localhost", 9090);
    ```

8.  使用以下代码包住您的业务逻辑。

    ```
    try {
      // 获取受保护的资源访问入口，参数为埋点资源名称。
      // 注意：必须定义一个变量保存入口对象，否则入口对象将被自动销毁并释放资源。
      sentinelEntry = $sentinel->entry("your-resource-name");
    
      // 在此处编写受保护的业务逻辑。
    } catch (\Sentinel\BlockException $e) {
      // 被Sentinel流控，在此处编写流控处理逻辑，如提示用户请求过多。
    } finally {
        // 将保存入口对象的变量置为null，使不再有变量引用入口对象，以销毁入口对象并释放资源。
        sentinelEntry = null;
    }
    ```

9.  重启您的PHP应用。


## 结果验证

登录[AHAS控制台](https://ahas.console.aliyun.com)，在左侧导航栏选择**流量防护** \> **应用防护**，若在应用防护页面出现该应用的资源卡片且有数据上报，则说明接入成功。

![应用防护.png](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/1733858951/p139423.png)

## 相关操作

PHP SDK目前支持流控规则、降级规则、隔离规则和系统规则：

-   [配置流控规则](/cn.zh-CN/流量防护/应用防护/配置规则/配置流控规则.md)
-   [配置降级规则](/cn.zh-CN/流量防护/应用防护/配置规则/配置降级规则.md)
-   [配置隔离规则](/cn.zh-CN/流量防护/应用防护/配置规则/配置隔离规则.md)
-   [自适应流控](/cn.zh-CN/流量防护/应用防护/配置规则/自适应流控.md)

