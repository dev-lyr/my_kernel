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

# 二 link:
## (1)概述:
- 功能: 网络设备配置.
- 语法: ip link {command|help},  man ip-link.
- command: add,delete,set,show,xstats,afstats.

## (2)add:
- 添加虚拟link.
- 类型: bridge,bond,vxlan,veth,vxlan,tap等.

# 三 netns
