# 通过 Java Agent 接入 {#concept_ejl_tw3_kgb .concept}

您可以通过 Java Agent（即 Java 探针）的方式，将应用接入 AHAS 控制台的流控降级服务。

## 操作引导 {#section_mqn_zjd_ggb .section}

您可以在 AHAS 控制台查看流控降级 Java Agent 接入的相关步骤。

1.  登录 [AHAS 控制台](https://ahas.console.aliyun.com/)。
2.  在控制台左上角，选择您的 Linux 主机所在的地域，分为以下两种情况：
    -   如果您的 Linux 主机在**北京**、**杭州**、**上海**或**深圳**的 VPC 网络中，在地域列表中选择对应的地域即可。
    -   如果不属于第一种情况，只要您的 Linux 主机有公网连接，在地域列表中，选择**公网**。
3.  在左侧导航栏，选择**流控降级**。

4.  在流控降级页面右上角，单击**添加应用**，选择**Java Agent 接入**页签，根据页面引导，安装 Java Agent。

![](https://aliware-images.oss-cn-hangzhou.aliyuncs.com/ahas/sc_java_agent.png)


## 安装 Java Agent（地域：北京、杭州、上海或深圳） {#section_nwf_by3_kgb .section}

如果您的 Linux 主机在**北京**、**杭州**、**上海**或**深圳**的 VPC 网络中，按照以下步骤接入。

根据 Java 虚拟机运行的环境，您可以选择一种方式来传入 Java Agent：

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

    2.  在 docker-compose.yaml 中添加以下配置项。如已有 JAVA\_OPTS，可将内容添加在后面。将 AppName 替换为您的应用名称。

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


接入成功后，在控制台左上角选择您的应用所在的地域。应用将以卡片方式显示在**流控降级**页面。

## 安装 Java Agent（地域：公网） {#section_v1s_qcj_kgb .section}

当您在地域列表中选择了**公网**，按照以下步骤接入 Java Agent。

**说明：** 在安装探针的过程中，需要使用 License。在控制台页面上的命令行中，已经自动分配了您的 License。

如果您按照本文中的步骤操作，请在控制台页面找到您的 License 并带入到以下命令行的 License 变量中。

通过在 Java 虚拟机中加载 Java 探针来识别 Java 应用，Java 应用名由传入的参数 AppName 来定义。根据 Java 虚拟机运行的环境，您可以从以下方式中选择一种方式来传入 Java 探针：

-   **方式一：非容器化应用服务器** 

    1.  确认文件 ahas-java-agent.jar 已经下载到主机的/opt/aliyunahas/agent目录下。通常，安装 AHAS 探针成功后，AHAS Java 探针也会随之下载到主机的 /opt/aliyunahas/agent目录下。
    2.  在应用 JVM 启动命令中，添加以下参数，将 AppName 替换为您的应用名称、license替换为控制台命令行提示中的唯一 license。

        ```
        -Dproject.name=AppName -Dahas.namespace=default -Dahas.license=license -javaagent:/opt/aliyunahas/agent/ahas-java-agent.jar
        ```

    3.  启动 JVM。
    **说明：** 更多具体示例，请查看控制台引导页面提示页面提示。

-   **方式二：Docker 容器** 
    1.  初始化 ahas-java-agent 容器。

        ```
        sudo docker pull \
        registry.cn-hangzhou.aliyuncs.com/ahascr-public/ahas-java-agent:latest && \
        docker run \
        --rm \
        --detach \
        --privileged=true \
        -v ahas-javaagent:/var/lib/aliyunahas/agent:rw \
        registry.cn-hangzhou.aliyuncs.com/ahascr-public/ahas-java-agent:latest
        ```

    2.  将 ahas-java-agent 挂载到相应的 Java 应用容器上。在 docker run 命令后面添加以下启动参数。如已有 JAVA\_OPTS，可将内容添加在后面。将AppName替换为您的应用名称、license 替换为控制台命令行提示中的唯一 license。

        ```
        -v ahas-javaagent:/var/lib/aliyunahas/agent:rw \
        --env JAVA_OPTS="-Dproject.name=AppName -Dahas.namespace=default -Dahas.license=license -javaagent:/var/lib/aliyunahas/agent/ahas-java-agent.jar"
        ```

-   **方式三：Docker Compose** 
    1.  初始化 ahas-java-agent 容器。

        ```
        sudo docker pull \
        registry.cn-hangzhou.aliyuncs.com/ahascr-public/ahas-java-agent:latest && \
        docker run \
        --rm \
        --detach \
        --privileged=true \
        -v ahas-javaagent:/var/lib/aliyunahas/agent:rw \
        registry.cn-hangzhou.aliyuncs.com/ahascr-public/ahas-java-agent:latest
        ```

    2.  在 docker-compose.yaml 中添加以下配置项。如已有 JAVA\_OPTS，可将内容添加在后面。将 AppName 替换为您的应用名称、license 替换为控制台命令行提示中的唯一 license。

        ```
        environment: 
        - JAVA_OPTS="-Dproject.name=AppName -Dahas.namespace=default -Dahas.license=license -javaagent:/var/lib/aliyunahas/agent/ahas-java-agent.jar"
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


接入成功后，在控制台左上角选择**公网**地域。应用将以卡片方式显示在**流控降级**页面。

## 后续操作 {#section_ckr_l2j_kgb .section}

接入了 AHAS 的流控降级服务后，您可以进一步了解：

-   [实时监控应用数据](../intl.zh-CN/流控降级/控制台指南/实时监控应用数据.md#)
-   [流控规则](../intl.zh-CN/流控降级/控制台指南/流控规则.md#)
-   [降级规则](../intl.zh-CN/流控降级/控制台指南/降级规则.md#)
-   [系统规则](../intl.zh-CN/流控降级/控制台指南/系统规则.md#)
-   [Java SDK 参考](../intl.zh-CN/流控降级/开发指南/Java SDK 参考/定义资源.md#)。

## 常见问题 {#section_tz5_42j_kgb .section}

如果您已完成流控降级服务接入，流控降级页面仍查看不到您的应用，可参考常见问题：[流控降级页面找不到应用](../intl.zh-CN/常见问题/流控降级常见问题.md#)。

