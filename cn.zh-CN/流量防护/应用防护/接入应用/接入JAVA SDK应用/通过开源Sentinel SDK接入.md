# 通过开源Sentinel SDK接入

通过开源组件Sentinel，可以便捷地接入AHAS应用防护。

## 操作步骤

使用开源组件Sentinel将应用接入AHAS应用防护以及连接控制台的具体操作，请参见[新手指南](https://github.com/alibaba/Sentinel/wiki/%E6%96%B0%E6%89%8B%E6%8C%87%E5%8D%97#%E5%85%AC%E7%BD%91-demo)。

若您已接入Sentinel控制台，您可以将Pom包中的`sentinel-transport-simple-http`模块替换为`ahas-sentinel-client`模块，接入AHAS应用防护。

**说明：** 若在本机或非阿里云VPC网络运行，请注意在AHAS控制台左上角选择地域为公网。

