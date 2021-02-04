# 为何Pod中仍存在已恢复故障的“僵尸进程”？

在K8s环境中，下发的故障已经被恢复了，但是Pod中仍存在该故障的“僵尸进程”。本文介绍该情况可能的原因以及解决方案。

## 可能原因

这是因为容器中存在PID Namespace隔离。在容器中，故障演练进程的父进程是PID=1的进程，容器中的一号进程不具有进程资源回收的能力，所以导致故障演练进程被终止之后，资源没有得到回收，从而成为僵尸进程。

## 解决方案

通过手动共享PID Namespace解决该问题。

在Pod的YAML文件中增加`shareProcessNamespace: true`，从而将Pod容器中PID=1的进程改为`/pause`进程，如下所示。

```
apiVersion: v1
kind: Pod
metadata:
  annotations:
    kubernetes.io/psp: ack.privileged
  labels:
    app: myapp
  name: myapp-pod
  namespace: ahas
spec:
  shareProcessNamespace: true
  containers:
  - command:
    - sh
    - -c
    - echo Hello Kubernetes! && sleep 3600
    image: busybox
    imagePullPolicy: Always
    name: myapp-container
    resources: {}
```

## 注意事项

共享PID Namespace会带来以下影响：

-   **容器进程不再具有PID 1。**

    在没有PID 1的情况下，一些容器镜像会拒绝启动（例如使用systemd的容器\)，或者拒绝执行`kill -HUP 1`之类的命令来通知容器进程。在具有共享进程命名空间的Pod中，如果执行`kill -HUP 1`，将会把消息通知到Pod沙箱（本文示例中的Pod沙箱即`/pause`）。

-   **进程对Pod中的其他容器可见。**

    包括`/proc`中可见的所有信息，例如作为参数或环境变量传递的密码，这些信息仅受常规Unix权限的保护。

-   **容器文件系统通过/proc/$pid/root链接对Pod中的其他容器可见。**

    这使调试更加容易，但也意味着文件系统安全性只受文件系统权限的保护。


