# 通过开源 Sentinel SDK 接入 {#concept_gsp_yw3_kgb .concept}

通过开源组件 Sentinel，可以便捷地接入 AHAS 应用流控降级。

## 操作步骤 {#section_59w_bjc_a5l .section}

使用开源组件 Sentinel 将应用接入 AHAS 应用刘空降及请参见[新手指南](https://github.com/alibaba/Sentinel/wiki/%E6%96%B0%E6%89%8B%E6%8C%87%E5%8D%97#%E5%85%AC%E7%BD%91-demo) 来连接 AHAS 流控降级控制台。

若您已接入 Sentinel 控制台，您可以将 Pom 包中的 `sentinel-transport-simple-http`模块替换为 `ahas-sentinel-client` 模块，接入 AHAS 应用流控降级。

**说明：**  若在本机或非阿里云 VPC 网络运行，请注意在 AHAS 控制台左上角选择地域 为 公网。

