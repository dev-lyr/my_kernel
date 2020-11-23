# 一 概述:
## (1)功能:
- 展示和操作routing,devices,policy routing和tunnels.

## (2)用法:
- ip [options] object {command | help}
- ip [-force] -batch filename

## (3)object:
- link
- address
- route
- rule
- neigh
- ntable
- tunnel
- netns
- 等等.

## (4)options:

## (5)备注:
- iproute2
- 通过netlink与内核交互.

# 二 link:
## (1)概述:
- 功能: 网络设备配置.
- 语法: ip link {command|help}, command: add,delete,set,show,xstats,afstats. 
- man ip-link.

## (2)type:
- bridge
- bridge_slave
- veth
- vxlan
- bond
- bond_slave
- 等等.

## (3)add:
- 功能: 添加virtual link.

## (4)set:
- 功能: 修改设备的属性.

## (5)show:
- 功能: 展示设备属性.

# 三 netns:
## (1)概述:
- 功能: 进程网络空间(network namespace)管理.
- 网络空间是网络stack的逻辑copy, 它有自己的路由,防火墙规则和网络设备.
- 默认情况下, 进程继承父进程的网络空间, 初始时所有进程共享同一个默认的网络空间(init process的).
- named网络空间: 通常是/var/run/netns/NAME下的一个可以打开的对象.
- 语法: ip [ OPTIONS ] netns  { COMMAND | help }

## (2)ip netns [list]:
- 功能: 显示所有named网络空间,会显示/var/run/netns下所有命名空间.

## (3)add/del/set

## (4)exec

# 四 address
