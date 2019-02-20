# RAM 子账号访问 AHAS 控制台 {#concept_100073_zh .concept}

AHAS 支持阿里云主子账号（RAM）访问体系。使用 RAM 子账号访问 AHAS 控制台前，您需要为该子账号开启控制台登录权限，并授权 **AliyunAHASFullAccess** 权限。

操作步骤如下：

1.  创建子账号，参考 [创建 RAM 用户](../../../../../intl.zh-CN/用户指南/身份管理/用户管理/用户.md#section_01)。
2.  启用子账号的控制台登录功能，并设置登录密码。参考[管理 RAM 用户](../../../../../intl.zh-CN/用户指南/身份管理/用户管理/用户.md#section_03)。
3.  授权子账号访问 AHAS 控制台，添加**AliyunAHASFullAccess**权限。参考[为 RAM 用户授权](../../../../../intl.zh-CN/快速入门/为 RAM 用户授权.md#)。

授权完成后，即可用子账号登录[子账号 AHAS 控制台](https://signin.aliyun.com/login.htm)。

