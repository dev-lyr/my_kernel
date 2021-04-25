# 一 概述:
## (1)net_cls子系统:
- Network Classsiffier cgroup: 提供一种给网络包打tag(classid)的接口.
- tc可用来给来自不同cgroups的包分配不同的优先级.
- netfilter也可以根据该tag来包上执行一些操作.

## (2)net_prio子系统:
- Network Priority cgroup提供一个让管理员来动态设置各应用网络流量优先级的接口.
