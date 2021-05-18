# MSHA服务关联角色

本文为您介绍MSHA服务关联角色（AliyunServiceRoleForMSHA）的应用场景以及如何删除服务关联角色。

MSHA服务关联角色（AliyunServiceRoleForMSHA）是为了完成MSHA自身的某个功能，需要获取其他云服务的访问权限，而提供的RAM角色。更多关于服务关联角色的信息请参见[服务关联角色](/cn.zh-CN/角色管理/服务关联角色.md)。

## 应用场景

MSHA在以下场景需要通过服务关联角色功能获取其他云服务资源的访问权限：

-   接入层集群管控功能需要访问ECS、SLB云服务的资源。
-   接入层域名管控功能需要访问云解析云服务的资源。
-   Kubernetes多活管控功能需要访问PrivateZone云服务及ACK云服务的资源。
-   数据层多活管控功能需要访问RDS、DRDS、DTS云服务的资源。
-   多活规则管控功能需要访问ACM云服务的资源。

## 权限说明

-   角色名称：AliyunServiceRoleForMSHA
-   角色权限策略：AliyunServiceRolePolicyForMSHA
-   权限说明：

    ```
    {
      "Version": "1",
      "Statement": [
        {
          "Effect": "Allow",
          "Action": [
            "ecs:DescribeInstances",
            "slb:DescribeLoadBalancers",
            "slb:DescribeLoadBalancerAttribute",
            "slb:AddBackendServers",
            "slb:RemoveBackendServers",
            "alidns:UpdateDNSSLBWeight",
            "alidns:SetDNSSLBStatus",
            "alidns:AddDomainRecord",
            "alidns:DeleteDomainRecord",
            "alidns:DescribeDomainRecords",
            "alidns:DescribeDomainInfo",
            "alidns:GetMainDomainName",
            "alidns:DescribeGtmInstanceAddressPool",
            "alidns:AddGtmAddressPool",
            "alidns:UpdateGtmAddressPool",
            "alidns:DeleteGtmAddressPool",
            "alidns:DescribeGtmInstances",
            "alidns:DescribeGtmInstance",
            "alidns:UpdateGtmInstanceGlobalConfig",
            "alidns:DescribeGtmAvailableAlertGroup",
            "alidns:DescribeGtmAccessStrategy",
            "alidns:DescribeGtmAccessStrategyAvailableConfig",
            "alidns:AddGtmAccessStrategy",
            "alidns:DeleteGtmAccessStrategy",
            "pvtz:DescribeZones",
            "pvtz:AddZone",
            "pvtz:AddZoneRecord",
            "pvtz:UpdateZoneRecord",
            "pvtz:DescribeZoneRecords",
            "pvtz:DeleteZoneRecord",
            "pvtz:DescribeZoneInfo",
            "cs:DescribeClusters",
            "cs:DescribeClusterUserKubeconfig",
            "rds:DescribeDBInstances",
            "rds:DescribeDatabases",
            "rds:DescribeDBInstanceAttribute",
            "rds:DescribeDBInstanceIPArrayList",
            "rds:ModifySecurityIps",
            "rds:DescribeTaskInfo",
            "rds:CreateAccount",
            "rds:DescribeAccounts",
            "rds:GrantAccountPrivilege",
            "rds:DescribeAccounts",
            "drds:DescribeDrdsInstances",
            "drds:DescribeDrdsDBs",
            "drds:DescribeRdsList",
            "drds:DescribeDrdsDbTablesTopology",
            "drds:DescribeTables",
            "dts:CreateSynchronizationJob",
            "dts:ConfigureSynchronizationJob",
            "dts:StartSynchronizationJob",
            "dts:SuspendSynchronizationJob",
            "dts:ModifySynchronizationObject",
            "dts:DeleteSynchronizationJob",
            "dts:DescribeSynchronizationJobStatus",
            "dts:DescribeSynchronizationJobs",
            "dts:DescribeSynchronizationObjectModifyStatus",
            "dts:DescribeSynchronizationJobStatusList",
            "dts:ConfigureSynchronizationJobReplicatorCompare",
            "dts:DescribeSynchronizationJobReplicatorCompare",
            "acms:*"
          ],
          "Resource": "*"
        },
        {
          "Action": "ram:DeleteServiceLinkedRole",
          "Resource": "*",
          "Effect": "Allow",
          "Condition": {
            "StringEquals": {
              "ram:ServiceName": "msha.aliyuncs.com"
            }
          }
        }
      ]
    }
    ```


## 删除服务关联角色

如果您需要删除AliyunServiceRoleForMSHA（服务关联角色），需要清除该角色对应主账号的所有多活命名空间。

-   清除每个多活命名空间下，接入层、数据层等每一层的资源配置。
-   在全局配置概览页面，清除所有多活命名空间。

1.  登录[RAM控制台](http://ram.console.aliyun.com)，在左侧导航栏中单击**RAM角色管理**。

2.  在RAM角色管理页面的搜索框中，输入**AliyunServiceRoleForMSHA**，自动搜索到名称为AliyunServiceRoleForMSHA的RAM角色。

3.  在右侧**操作**列，单击**删除**。

4.  在删除RAM角色对话框，单击**确定**。

    **说明：** 删除服务关联角色后会影响您MSHA数据的获取，请谨慎删除！


