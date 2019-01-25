# 阿里云 ECS 主机接入 {#concept_xw3_z3y_ngb .concept}

通过一键安装 AHAS 探针，可快速将阿里云环境中的 ECS 主机（Linux）接入 AHAS 控制台，查看其系统架构、进行故障测评；通过安装 Java 探针，可同时使用流控降级等功能。

## 前提条件 {#section_hpc_5yy_ngb .section}

已[开通 AHAS 服务](../../../../../intl.zh-CN/.md#)。

## 选择地域 {#section_fdp_jky_ngb .section}

接入阿里云 VPC 网络的 Linux 主机前，需在控制台选择对应的地域。

1.  登录 [AHAS 控制台](https://ahas.console.aliyun.com/)。

2.  在控制台左上角，选择您的主机所在的地域。

    **说明：** 已开通的地域包括北京、杭州、深圳，其他地域陆续开放中；目前，其他地域的阿里云 ECS 主机可以通过“公网”地域接入，接入方式可参考[普通 Linux 主机接入](intl.zh-CN/架构感知/接入/普通 Linux 主机接入.md#)。

3.  （可选）每个地域会有一个默认（Default）环境，您也可以添加自定义环境，如开发环境、测试环境等。
    1.  单击概览页面左上角的下拉列表，单击**添加环境**。

        ![](https://aliware-images.oss-cn-hangzhou.aliyuncs.com/ahas/sc_env_selection.png) 

    2.  填写环境名称，单击**确定**。添加完成后，即可以在刚刚添加的环境中进行操作。

        如需切换，单击左上角下拉菜单，选择其他环境。


## 安装探针（地域：北京、杭州或深圳） {#section_yyy_gjv_cgb .section}

按照下面的操作步骤为阿里云 ECS 主机安装应用高可用探针和 Java 探针，接入 AHAS 控制台。

1.  在 AHAS 控制台的**概览**页，单击**架构感知**模块下的**接入向导**。

    ![](https://aliware-images.oss-cn-hangzhou.aliyuncs.com/ahas/sc_ecs_agent_installation_overview.png)

2.  在**选择环境**页签下，单击**阿里云 ECS** 作为您要安装的环境。

    ![](https://aliware-images.oss-cn-hangzhou.aliyuncs.com/ahas/pg_wizard_1.png)

3.  在**安装应用高可用探针**页签下，列出了您账号下所有的 ECS 主机。按需执行以下操作之一，然后单击**下一步**。

    -   如需为单台主机安装探针，请单击右侧**操作**栏中的**单击安装**。
    -   如需为多台主机批量安装探针，请勾选目标主机左侧的复选框，并在页面左下角单击**批量安装**。
    ![](https://aliware-images.oss-cn-hangzhou.aliyuncs.com/ahas/pg_wizard_2.png)

4.  单击**下一步**。
5.  如果需要同时使用流控降级功能，则需要安装 Java 探针；否则可跳过。

    根据 Java 虚拟机运行的环境，您可以从以下方式中选择一种方式来传入 Java 探针：

    -   **方式一：非容器化应用服务器**

        1.  确认文件 ahas-java-agent.jar 已经下载到主机的/opt/aliyunahas/agent目录下。通常，安装 AHAS 探针成功后，AHAS Java 探针也会随之下载到主机的 /opt/aliyunahas/agent目录下。
        2.  在应用 JVM 启动命令中，添加以下参数，将 AppName 替换为您的应用名称。

            ```
            -Dproject.name=AppName -Dahas.namespace=default -javaagent:/opt/aliyunahas/agent/ahas-java-agent.jar
            ```

        3.  启动 JVM。
        **说明：** 更多具体示例，请查看控制台引导页面提示。

    -   **方式二：Docker 容器**
        1.  初始化 ahas-java-agent 容器。

            ```
            sudo docker pull \
            registry.cn-hangzhou.aliyuncs.com/ahascr/ahas-java-agent:latest && \
            docker run \
            --rm \
            --detach \
            --privileged=true \
            -v ahas-javaagent:/var/lib/aliyunahas/agent:rw \
            registry.cn-hangzhou.aliyuncs.com/ahascr/ahas-java-agent:latest
            ```

        2.  将 ahas-java-agent 挂载到相应的 Java 应用容器上。在 docker run命令后面添加以下启动参数。如已有 JAVA\_OPTS，可将内容添加在后面。将 AppName 替换为您的应用名称。

            ```
            -v ahas-javaagent:/var/lib/aliyunahas/agent:rw \
            --env JAVA_OPTS="-Dproject.name=AppName -Dahas.namespace=default -javaagent:/var/lib/aliyunahas/agent/ahas-java-agent.jar"
            ```

    -   **方式三：Docker Compose**
        1.  初始化 ahas-java-agent 容器。

            ```
            sudo docker pull \
            registry.cn-hangzhou.aliyuncs.com/ahascr/ahas-java-agent:latest && \
            docker run \
            --rm \
            --detach \
            --privileged=true \
            -v ahas-javaagent:/var/lib/aliyunahas/agent:rw \
            registry.cn-hangzhou.aliyuncs.com/ahascr/ahas-java-agent:latest
            ```

        2.  在 docker-compose.yaml 中添加以下配置项。如已有JAVA\_OPTS，可将内容添加在后面。将 AppName 替换为您的应用名称。

            ```
            environment: 
            - JAVA_OPTS="-Dproject.name=AppName -Dahas.namespace=default -javaagent:/var/lib/aliyunahas/agent/ahas-java-agent.jar"
            volumes:
            - ahas-javaagent:/var/lib/aliyunahas/agent:rw
            ```

        3.  在 docker-compose.yaml 文件的最后面添加以下内容。

            ```
            volumes:
             ahas-javaagent:
              external: true
            ```

        4.  重启 Docker Compose。

            ```
            docker-compose up --build -d
            ```


## 后续操作 {#section_sxn_k2z_ngb .section}

接入成功后，您可以执行操作：

-   [查看系统架构](intl.zh-CN/架构感知/查看系统架构.md#)
-   [测评应用的高可用能力](../../../../../intl.zh-CN/.md#)
-   [实时监控应用数据](../../../../../intl.zh-CN/流控降级/控制台指南/实时监控应用数据.md#)

