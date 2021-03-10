# 授权RAM用户

通过在访问控制RAM控制台创建的RAM用户，您可以实现权限分割的目的，按需为RAM用户赋予不同权限。本文介绍如何创建并授权RAM用户。

[开通MSHA](/cn.zh-CN/多活容灾/用户指南/开通MSHA.md)

出于安全考虑，您可以为阿里云账号创建RAM用户，并根据需要为这些RAM用户赋予不同的权限，这样就能在不暴露阿里云账号密钥的情况下，实现让RAM用户各司其职的目的。

在本文中，假设企业A希望让部分员工处理日常运维工作，则企业A可以创建RAM用户，并为RAM用户赋予相应权限，此后员工即可使用这些RAM用户登录控制台。

MSHA支持借助RAM用户实现分权，为RAM用户开启控制台登录权限，并按需授予以下权限：

-   AliyunMSHAFullAccess：MSHA的完整权限。
-   AliyunMSHAReadOnlyAccess：MSHA的只读权限。

## 步骤一：创建RAM用户

首先需要使用阿里云账号登录RAM控制台并创建RAM用户。

1.  登录[RAM控制台](http://ram.console.aliyun.com)，在左侧导航栏中选择**人员管理** \> **用户**，并在用户页面单击**创建用户**。

2.  在创建用户页面，输入**登录名称**和**显示名称**。

    如需一次创建多个用户，则单击**+添加用户**。

    **说明：** 登录名称中允许使用小写英文字母、数字、半角句号（.）、下划线（\_）和短划线（-），长度不超过128个字符。显示名称不可超过24个字符或汉字。

3.  设置访问方式，然后单击**确定**。

    -   如果选中**控制台访问**，则完成进一步设置，包括自动生成密码或自定义登录密码、登录时是否要求重置密码，以及是否开启MFA多因素认证。
    -   如果选中**编程访问**，则RAM会自动为RAM用户创建AccessKey（API访问密钥）。

        **说明：**

        -   为提高安全性，请选择一种访问方式。
        -   出于安全考虑，RAM控制台只提供一次查看或下载AccessKey Secret的机会，即创建AccessKey时。因此请务必将AccessKey Secret记录到安全的地方。

## 步骤二：为RAM用户添加权限

在使用RAM用户之前，需要为其添加相应权限。

1.  在[RAM控制台](http://ram.console.aliyun.com)左侧导航栏选择**人员管理** \> **用户**。

2.  在**用户**页面上找到需要授权的用户，单击**操作**列中的**添加权限**。

3.  在**添加权限**面板的**选择权限**区域中，通过关键字搜索需要添加的权限策略（**AliyunMSHAFullAccess**） ，并单击权限策略将其添加至右侧的**已选择**列表中，然后单击**确定**。

4.  若没有搜索到相关权限策略或有更精细化的权限设置要求，单击**+新建权限策略**。在新建自定义权限策略页面，填写**策略名称**，选择**配置模式**为**脚本配置**，在策略内容中输入权限策略，然后单击**确定**。

    MSHA支持的自定义模板如下：

    -   对授权RAM用户允许对所有MHSA命名空间进行操作。

        ```
        {
            "Statement": [
                {
                    "Effect": "Allow",
                    "Action": "msha:*",
                    "Resource": "*"
                }
            ],
            "Version": "1"
        }
        ```

    -   对授权RAM用户允许对指定命名空间可进行任意操作。

        ```
        {
            "Statement": [
                {
                    "Effect": "Allow",
                    "Action": "msha:*",
                    "Resource": [
                        "acs:msha:*:*:mshaTenantId/<mshaTenantId1>",
                        "acs:msha:*:*:mshaTenantId/<mshaTenantId2>"
                    ]
                }
            ],
            "Version": "1"
        }
        ```

        **说明：** <mshaTenantId1\>、<mshaTenantId2\>输入指定命名空间MSHATenant ID值。

    -   对授权RAM用户允许对指定命名空间可进行读操作。

        ```
        {
            "Statement": [
                {
                    "Effect": "Allow",
                    "Action": "msha:query*",
                    "Resource": [
                        "acs:msha:*:*:mshaTenantId/<mshaTenantId1>",
                        "acs:msha:*:*:mshaTenantId/<mshaTenantId2>"
                    ]
                }
            ],
            "Version": "1"
        }
        ```

        **说明：** <mshaTenantId1\>、<mshaTenantId2\>输入指定命名空间MSHATenant ID值。

    新建权限策略完成后，在添加权限面板中，单击**自定义策略**页签，通过关键字搜索需要添加的权限策略，并单击权限策略将其添加至右侧的**已选择**列表中，然后单击**确定**。

5.  在**添加权限**的授权结果面板，查看授权信息摘要，并单击**完成**。


## 使用RAM用户登录控制台

使用阿里云账号创建好RAM用户后，即可将RAM用户的登录名称及密码或者AccessKey信息分发给其他用户。其他用户可以按照以下步骤使用RAM用户登录AHAS控制台。

1.  登录[RAM用户登录入口](https://signin.aliyun.com/login.htm)。

2.  在RAM用户登录页面上，输入RAM用户登录名称，单击**下一步**，并输入RAM用户密码，然后单击**登录**。

    **说明：** RAM用户登录名称的格式为<$username\>@<$AccountAlias\>或<$username\>@<$AccountAlias\>.onaliyun.com。<$AccountAlias\>为账号别名，如果没有设置账号别名，则默认值为阿里云账号的ID。

3.  在RAM用户中心页面上搜索并单击**应用高可用服务**或**AHAS**，即可访问应用高可用服务控制台，然后在左侧导航栏选择**多活容灾**。


