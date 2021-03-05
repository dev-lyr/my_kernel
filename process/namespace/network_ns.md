# 一 概述:
## (1)概述:
- 网络命名空间提供网络相关的系统资源的隔离: 网络设备,IPv4和IPv6协议栈,IP路由表,/proc/net目录,/sys/class/net目录,/proc/sys/net下多种文件,port端口等等.
- 使用网络空间需要kernel配置CONFIG_NET_NS选项.
- 物理设备只能在一个网络空间中live,当网络空间被释放(例如:当网络空间中最后一个进程终止),它的物理设备会被移动到initial网络空间.

## (2)使用:
- ip netns

## (3)备注:
- net/core/net_namespace.c
- include/net/net_namespace.h
- man network_namespaces

