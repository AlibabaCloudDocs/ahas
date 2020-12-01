# 配置RAM权限

AHAS支持对云服务器ECS（Elastic Compute Service）和容器服务ACK（Alibaba Cloud Container Service for Kubernetes）进行演练，为了控制被演练对象的范围，AHAS故障演练支持对RAM子账号进行授权配置。

## 配置方法

1.  登录[RAM访问控制](https://ram.console.aliyun.com/)。

2.  在左侧导航栏中选择**权限管理** \> **权限策略管理**。

3.  在权限策略管理页面，单击**创建权限策略**。

4.  在新建自定义权限策略页面，填写**策略名称**，在**配置模式**下选择**脚本配置**。

5.  在策略内容中填写脚本。

    以如下配置为例进行说明。

    ```
    {
        "Statement": [
            {
                "Effect": "Allow",
                "Action": "ahas:*",
                "Resource": [
                  "acs:ecs:*:*:*",
                  "acs:cs:*:*:*"
                ]
            }
        ],
        "Version": "1"
    }
    ```

    -   Action：配置为ahas:\* 拥有资源的全部权限。
        -   创建演练权限：配置为`ahas:CreateExperiment`，授予该权限后，可以对资源进行演练配置操作（含更新操作）。
        -   执行演练权限：配置为`ahas:ExecuteExperiment`，授予该权限后，可对资源进行演练执行操作（演练可执行的条件为“子账号拥有该演练中所有资源的执行权限”）。
    -   Resource：目前仅支持ECS和ACK两种资源，请根据实际情况配置允许演练的资源，具体语法请参见[创建自定义策略](/cn.zh-CN/权限策略管理/自定义策略/创建自定义策略.md)说明。
6.  授权新创建的权限策略给用户，详情请参见[为RAM用户授权](/cn.zh-CN/用户管理/为RAM用户授权.md)。


## 应用权限配置方法

**说明：** 应用及应用分组名称不可包含中文。

应用对应的权限配置方法请参见以下操作步骤。

1.  登录[RAM访问控制](https://ram.console.aliyun.com/)。

2.  在左侧导航栏中选择**权限管理** \> **权限策略管理**。

3.  在权限策略管理页面，单击**创建权限策略**。

4.  在新建自定义权限策略页面，填写**策略名称**，在**配置模式**下选择**脚本配置**。

5.  在策略内容中填写脚本。

    ```
    {
        "Statement": [
            {
                "Effect": "Allow",
                "Action": "ahas:*",
                "Resource": "acs:ahas:*:*:*"
            }
        ],
        "Version": "1"
    }
    ```

    -   Action：配置为ahas:\* 拥有资源的全部权限。
        -   创建演练权限：配置为`ahas:CreateExperiment`，授予该权限后，可以对资源进行演练配置操作（含更新操作）。
        -   执行演练权限：配置为`ahas:ExecuteExperiment`，授予该权限后，可对资源进行演练执行操作（演练可执行的条件为“子账号拥有该演练中所有资源的执行权限”）。
    -   Resource：支持按应用和应用分组进行资源划分，以不同维度配置授权。
    -   Resource表达式格式：

        ```
        acs:ahas:region:accountId:environment/appInstance/appGroup/ip
        ```

    -   Resource表达式说明：
        -   accountId：用户ID。
        -   environment：环境。指AHAS平台上的环境，取值是环境名，例如默认的default。
        -   appInstance：应用。用户部署故障演练探针时确定，如果用户部署时不指定，会归属为默认应用（ahas-default-app）。
        -   appGroup：应用分组。用户部署故障演练探针时确定，如果用户部署时不指定，会归属为默认应用分组（ahas-default-app-group）。
        -   ip：资源IP，如ecs ip，pod ip或node ip等。

## 示例

**示例1**

```
{
    "Statement": [
        {
            "Effect": "Allow",
            "Action": "ahas:CreateExperiment",
            "Resource": "acs:ahas:*:*:online/business/business_host/*"
        }
    ],
    "Version": "1"
}
```

如上示例1所示，持有该权限的人对**online环境 -\> business应用 -\> business\_host分组**内所有资源拥有配置及更新权限。

**示例2**

```
{
    "Statement": [
        {
            "Effect": "Allow",
            "Action": "ahas:ExecuteExperiment",
            "Resource": "acs:ahas:*:*:default/order/order_1/10.1.0.1"
        }
    ],
    "Version": "1"
}
```

如上示例2所示，持有该权限的人对**default环境 -\> order应用 -\> order\_1分组 -\> 10.1.0.1设备**拥有演练执行权限。

