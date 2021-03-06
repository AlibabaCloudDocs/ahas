# 如何理解并发、QPS和RT的关系？

本文介绍并发、QPS和RT的概念及其之间的关系。

在应用防护的数据图中，您可以看到每个接口都有以下3个指标：

-   QPS：Query per Second，直接反应应用吞吐能力的指标。
-   RT：Response Time，响应时间，表示处理请求快慢的指标。
-   并发：表示处理请求耗费的并发线程数。

如果处理能力弱，则响应时间长，即RT值较高。相同过来的请求，会导致并发线程数增加，QPS也会有所降低。如下图所示。

![FAQ QPS](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/5926752061/p172783.png)

并发在不同的场景中表示不同的概念，例如以下场景：

-   压测中施压并发指并发虚拟用户数。
-   SLB的并发指并发连接数。
-   服务端统计的并发指并发线程数。
-   流控规则中的并发指该资源正在执行的线程数，线程数模式按照资源的并发线程数进行流量控制。

关于压测的并发虚拟用户数和SLB的并发连接数概念，请参见[FAQ]()。

