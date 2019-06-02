# 一 概述
## (1)功能:
- 存储数据包, 在所有网络层次都用该结构来存储其报头，用户数据(有效负载)以及其它内部信息.
- 定义: include/linux/skbuff.h

# 二 常用字段:
## (1)布局字段:
- struct sk_buff *next, *prev: 内核使用双向链表来维护所有sk_buff结构.
- struct rb_node *rnnode: 对tcp/netem的另一个选择.

## (2)struct sock * sk
- 拥有的socket, 网络层的socket结构, 详见include/net/sock.h.
- 相关: struct socket, 详见include/linux/net.h

## (3)struct net_device * dev
- 每种网络设备(真实设备(如NIC)或虚拟设备(Bonding或VLAN))都用这个数据结构表示, 包括软硬件配置信息等.
- 详见include/linux/netdevice.h.

## (4)相关首部:
- transport_header: 传输层首部.
- inner_transport_header
- network_header: 网络层首部.
- inner_network_header
- mac_header: 链路层首部.
- inner_mac_header