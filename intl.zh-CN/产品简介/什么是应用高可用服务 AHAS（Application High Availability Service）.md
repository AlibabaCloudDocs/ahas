# 什么是应用高可用服务 AHAS（Application High Availability Service） {#concept_erb_lkb_kgb .concept}

应用高可用服务（Application High Availability Service）是一款专注于提高应用高可用能力的 SaaS 产品，包含架构感知、故障演练和流控降级（即限流降级）三大独立的功能模块。

-   [架构感知](intl.zh-CN/产品简介/什么是应用高可用服务 AHAS（Application High Availability Service）.md#section_adl_vwb_kgb)：
    -   自动感知应用的拓扑结构
    -   以可视化的方式直观呈现应用对基础架构的依赖关系和组件间的依赖关系
    -   持续记录上述依赖关系
-   [故障演练](intl.zh-CN/产品简介/什么是应用高可用服务 AHAS（Application High Availability Service）.md#section_lbt_wwb_kgb)：
    -   提供基于真实线上故障的高可用能力演练服务
    -   根据您的应用架构智能推荐故障演练场景
-   [流控降级](intl.zh-CN/产品简介/什么是应用高可用服务 AHAS（Application High Availability Service）.md#section_wkt_xwb_kgb)：
    -   专业化多样化的限流手段
    -   实时秒级的监控
    -   立即生效的规则管理

## 架构感知 {#section_adl_vwb_kgb .section}

-   **功能**

    服务器、存储、网络是现代云平台的基础设施。随着上云战略的推进，越来越多的大型企业将业务、服务、系统构建在云平台上。开源软件和云服务的多样性，开发语言的异构性，以及企业 IT 团队的组织和能力差异，都提高了标准化的复杂性。

    在此背景下，架构感知功能应运而生。它会采集和分析操作系统及第三方标准接口，捕捉进程级的调用关系，并使用特征库算法识别进程所使用的技术组件，最后在服务器、容器和进程这三个维度上以可视化的方式展示应用架构。

-   **数据源**

    AHAS 支持的数据源如下表所示。

    ![AHAS 支持的数据源](http://aliware-images.oss-cn-hangzhou.aliyuncs.com/ahas/dg_data_sources.png "AHAS 支持的数据源")

-   **工作流程**

    AHAS 架构感知的工作流程包括四个步骤：

    1.  数据采集
    2.  关系构建
    3.  特征识别
    4.  架构可视化
    ![架构感知工作流程](http://aliware-images.oss-cn-hangzhou.aliyuncs.com/ahas/dg_arch_detect_workflow.png "架构感知工作流程")

-   **界面展现**

    ![架构感知](http://aliware-images.oss-cn-hangzhou.aliyuncs.com/ahas/ex_arch_visulization.png "架构可视化")


## 故障演练 {#section_lbt_wwb_kgb .section}

-   **功能**

    根据架构感知模块捕捉到的架构数据主动制造故障，检验应用系统及其各组件在故障下的可用性表现，从而验证应用系统的高可用能力，提前暴露故障隐患，帮助您针对性地应对风险。

-   **工作流程**

    ![故障演练工作流程](http://aliware-images.oss-cn-hangzhou.aliyuncs.com/ahas/dg_test_workflow.png "故障演练工作流程")

    如图所示，故障演练评模块的工作流程为：

    1.  架构感知：根据架构感知模块对命令行、依赖等的分析，识别出系统中的实例和组件。
    2.  能力映射：将组件与高可用能力模型中的架构准则和能力进行映射。
    3.  场景映射：将高可用能力和标类场景进行映射。
    4.  演练执行：通过上述步骤明确系统稳定性要求，找出有针对性的故障演练然后通过流程化的故障演练引导您执行推荐的故障演练任务。
    5.  故障演练报告：故障演练任务完成后，以故障演练报告总结故障演练结果。

![故障演练](https://aliware-images.oss-cn-hangzhou.aliyuncs.com/ahas/ex_fault_testing.png "故障演练")

## 流控降级 {#section_wkt_xwb_kgb .section}

-   **功能**

    在当今日益复杂的应用环境下，应用设计应该遵循“面向失败”的设计原则，对上下游的依赖零信任。借助流量控制、熔断降级模块，您的应用有能力对流量采取限流控制，并对下游依赖进行降级处理。

-   **工作流程**

    流控降级模块支持主流的 Java 框架，包括 HTTP 和 Dubbo。该模块可以实时监控框架的 QPS（Queries per Second，每秒查询数）、线程数、响应时间、异常数等指标，并有选择地截断对这些框架的访问，从而保护应用的可用性。此外，利用 AHAS 提供的 SDK，您还可以采取更细粒度的代码级限流降级防护措施。

    ![流控降级工作流程](http://aliware-images.oss-cn-hangzhou.aliyuncs.com/ahas/dg_safeguarding_workflow.png "流控降级工作流程")


![流控降级界面](https://aliware-images.oss-cn-hangzhou.aliyuncs.com/ahas/pg_safeguarding.png "流控降级")

## AHAS 使用场景 {#section_bz2_htv_1fb .section}

-   **微服务高可用**

    如今，Spring Cloud、Kubernetes 的微服务架构对服务的高可用性提出了前所未有的挑战。借助 AHAS，您可以在零代码改动的前提下，快速使用 SaaS 化的高可用服务，包括架构可视化、架构变化追踪、故障演练和流控降级保护。

    AHAS 支持 Spring Cloud 组件的快速发现、故障演练能力，以及 SpringBoot 应用的一键流控降级。

    AHAS 支持阿里云容器服务 Kubernetes 应用的快速接入。

-   **传统应用高可用**

    由于缺乏高可用能力，对于传统的 Java 单体应用和分布式应用而言，如何保障稳定性和连续性向来是个难题。

    AHAS 提供了应用高可用保障所必需的架构实时展现与追踪、架构高可用性故障演练，以及 Java 应用零代码改动接入流控降级的能力。即便是已上线的应用，也无需升级改造。此外，对于引入的开源或第三方组件，AHAS 可以进行自动化智能评估，并提供优化使用方面的指导。​


## 相关文档 {#section_hkb_fvv_1fb .section}

-   [第三方组件和云服务支持列表](../intl.zh-CN/架构感知/第三方组件和云服务支持列表.md#)

