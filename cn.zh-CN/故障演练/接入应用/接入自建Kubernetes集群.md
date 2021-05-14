# 接入自建Kubernetes集群

AHAS架构感知和故障演练支持接入自建Kubernetes集群，可以自动侦测容器环境包含的ECS主机、容器组、容器、进程等。本文介绍如何将探针接入自建Kubernetes集群。

## 前提条件

确保您的Kubernetes api-server组件接口版本在1.10及以上。

## 操作步骤

1.  登录[AHAS控制台](https://ahas.console.aliyun.com)，在顶部导航栏选择集群所在地域。

    **说明：**

    -   对于阿里云VPC环境的Kubernetes集群，已开通的地域包括华南1（深圳）、华北2（北京）、华东2（上海）、华北3（张家口）、华东1（杭州）。其他地域的用户，可以通过公网地域接入。
    -   如果您的Kubernetes应用有公网连接，均可通过选择公网地域接入AHAS控制台。
2.  在左侧导航栏选择**探针管理**。
3.  在探针管理页面上方的下拉列表中，选择**添加环境**，并在添加环境对话框中填写环境名称。

    **说明：** 每个地域会有一个默认（Default）环境。您也可以添加自定义环境，如开发环境、测试环境等。不同环境的资源逻辑隔离。

    ![添加环境2.png](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/8973790261/p273733.png)

4.  在探针管理页面，选择**探针安装** \> **安装故障演练探针**。
5.  在安装探针页面，单击**自建Kubernetes**。
6.  选择以下任意一种方式安装Helm Chart包。
    -   单击下载[Helm Chart包](https://ahasoss-cn-zhangjiakou.oss-cn-zhangjiakou.aliyuncs.com/agent/prod/1.13.2/ahas-1.13.2.tgz?spm=5176.11961263.0.0.60d63bc1IlH2PZ&file=ahas-1.13.2.tgz)。
    -   执行相应的命令下载。
7.  安装高可用探针。

    -   Helm v2安装探针：
        -   非公网：

            ```
            helm install --set env.name=default --set controller.cluster_id=<替换为集群ID，取值无特殊要求> --set controller.cluster_name=<替换为集群名称，取值无特殊要求> --namespace ahas --name ahas ahas-1.13.2.tgz
            ```

        -   公网：

            ```
            helm install --set env.name=default --set license=<替换为真实license> --set controller.cluster_id=<替换为集群ID，取值无特殊要求> --set controller.cluster_name=<替换为集群名称，取值无特殊要求> --namespace ahas --name ahas ahas-1.13.2.tgz
            ```

    -   Helm v3安装探针：
        -   非公网：

            ```
            helm install ahas ahas-1.13.2.tgz --namespace ahas --set env.name=default,controller.cluster_id=<替换为集群ID，取值无特殊要求>,controller.cluster_name=<替换为集群名称，取值无特殊要求>
            ```

        -   公网：

            ```
            helm install ahas ahas-1.13.2.tgz --namespace ahas --set env.name=default,license=<替换为真实license>,controller.cluster_id=<替换为集群id，取值无特殊要求>,controller.cluster_name=<替换为集群名字，取值无特殊要求>
            ```

    执行成功后，返回如下：

    ![返回执行](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/9652698951/p47687.png)

8.  在安装探针页面单击**下一步**，并在查看数据页面检查已安装的探针信息。单击**完成**。



## 结果验证

创建完成后，您可以登录[AHAS控制台](https://ahas.console.aliyun.com)，在左侧导航栏选择**探针管理**，在探针管理页面单击**Kubernetes**页签，可查看到接入的集群名称以及探针信息。

