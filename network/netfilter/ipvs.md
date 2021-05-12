# 一 概述:
## (1)概述:
- ipvs(IP Virtual Server): 实现传输层的负载平衡,是lvs的组成部分.
- ipvs在netfilter之上构造和使用.
- lvs可基于集群中的2个或多个节点构造一个可扩展的网络服务, 集群中的active node 重定向服务请求到真正执行服务的server hosts集合.
- 支持2中协议(tcp和udp), 

## (2)package-forwarding方法:
- NAT
- tunneling
- direct routing)

## (3)负载平衡算法(8种):

## (4)相关命令:
- ipvsadm: 用于创建,维护和检查内核中的虚拟服务器表.
- ipvsadm-restore
- ipvsdam-save

## (5)备注:
- https://en.wikipedia.org/wiki/IP_Virtual_Server
- Documentation/networking/ipvs-sysctl.md
- net/netfilter/ipvs
- /proc/net

# 二 ipvsadm:
## (1)概述:
- ipvsadm用来创建,维护和检查kernel中的virtual server table.

## (2)相关命令:
- -A/--add-service: 添加一个virtual service.
- -E/--edit-service
- -D/--delete-service
- -C/--clear: clear vitual server table.
- -S/--save
- -R/--restore
- -L/--list/-l
- -Z/--zero
- -a/--add-server
- -e/--edit-server
- -d/--delete-server
- --start-daemon
- --stop-daemon

## (3)参数:
- -t/--tcp-service
- -u/--udp-service
- -s/--scheduler: 调度方法.
- -r/--real-server
