# Nginx接入Sidecar根据文档操作还是提示不兼容怎么办？

## Condition

按照[接入Nginx](/cn.zh-CN/Nginx防护/接入Nginx.md)文档中的步骤[4](/cn.zh-CN/Nginx防护/接入Nginx.mdstep_541_s40_vlx)操作，在CentOS 7操作系统下，Nginx版本为nginx-1.16.1，使用对应动态模块路径的lib/centos7-nginx-1.16.1/ngx\_sentinel\_module.so，但系统还是提示Nginx不兼容。如下图所示。

![Nginx](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/8043372061/p173415.png)

## Cause

Nginx自身限制编译动态模块.so文件时的Nginx版本和编译配置必须相同才兼容。当Nginx接入Sidecar时操作系统相同、Nginx版本相同，但编译配置不同时，也可能会不兼容Nginx。Sidecar安装包附带的.so版本是根据Yum EPEL仓库的Nginx打包的，如果使用从Yum EPEL安装的Nginx版本就可以使用默认提供的.so版本。

## Remedy

1.  如果遇到类似不兼容的情况，请您把`Nginx -V`（大写的V）输出的完整文本复制到用户钉钉群（群号：23196438）中，并联系我们，我们会为您单独提供一份对应的专属.so模块。


