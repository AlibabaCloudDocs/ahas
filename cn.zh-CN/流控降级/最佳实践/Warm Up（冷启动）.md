# Warm Up（冷启动） {#concept_pmt_m4b_mgb .concept}

Warm Up，即冷启动/预热的方式。当系统长期处于低水位的情况下，流量突然增加时，直接把系统拉升到高水位可能瞬间把系统压垮。通过"冷启动"，让通过的流量缓慢增加，在一定时间内逐渐增加到阈值上限，给冷系统一个预热的时间，避免冷系统被压垮。

## 原理 {#section_e13_n4b_mgb .section}

冷启动，参考了 [Guava](https://github.com/google/guava/blob/master/guava/src/com/google/common/util/concurrent/SmoothRateLimiter.java) 的算法，通过随时调整斜率，把流量在指定的时间之类缓慢调整到特定的阈值。

## 效果 {#section_f13_n4b_mgb .section}

通过设定规则之后，可以看到流量的增长趋势如下图所示：

![](https://aliware-images.oss-cn-hangzhou.aliyuncs.com/ahas/sc_example_warmup.png) 

## 配置流控规则 {#section_l1q_lwh_mgb .section}

在流控规则中，选择**Warm Up**，并且在预热时间内填写期望系统热起来的时间即可。

![](https://aliware-images.oss-cn-hangzhou.aliyuncs.com/ahas/db_bestp_warmup.png) 

具体操作步骤，参见[新建流控规则](intl.zh-CN/流控降级/控制台指南/流控规则.md#section_yks_qfd_kgb)。

