# 一 概述:
## (1)概述:
- 默认情况下, 一个进程会继承它的父进程的网络namespace, 最初所有进程共享同样的来自init进程的默认网络namespace.
- 网络命名空间提供网络相关的系统资源的隔离: 
- 使用网络空间需要kernel配置CONFIG_NET_NS选项.
- 物理设备只能在一个网络空间中live,当网络空间被释放(例如:当网络空间中最后一个进程终止),它的物理设备会被移动到initial网络空间.

## (2)隔离的资源:
- 网络设备
- IPv4和IPv6协议栈
- IP路由表
- /proc/net目录
- /sys/class/net目录
- /proc/sys/net下多种文件
- port端口
- 等等.

## (3)使用:
- ip netns
- setns

## (4)备注:
- net/core/net_namespace.c
- include/net/net_namespace.h
- man network_namespaces
- /proc/<pid>/ns/

# 二 ip netns:
## (1)概述:
- 进程网络namespace管理.
- 目录: /var/run/netns

## (2)ip netns add/list/delete:
- add: 创建一个named网络namespace.
- list: 显示所有named网络namespace.
- delete

## (3)ip netns exec:
- 功能: 在一个named网络namespace中执行命令.

