# 一 概述:
## (1)概述:
- 部分协议是系统内在的, 部分是以模块时候加载的, 系统内在的在系统初始化时候注册协议处理函数(net/ipv4/af_inet.c), 模块则是在模块加载时.
- 接收方的协议处理函数.

# 二 网络层:
## (1)协议处理函数的注册:
- 当一个协议注册时, 内核会调用**dev_add_pack**注册协议处理函数, 参数为协议相关的packet_type, 例如: ip_packet_type.

## (2)选择协议处理函数:
- 驱动程序接收到帧时, 会将其保存在sk_buff结构中, sk_buff的protocol会被初始化, 该字段值会由netif_receive_sbk函数来查询以确定使用哪个网络层函数来处理该帧.
- protocol字段的值参考: include/linux/if_ether.h中ETH_P_XXX.

## (3)相关结构:
- packet_type:每个协议相关处理函数都由packet_type结构(netdevice.h)表示, 例如: ip_packet_type(net/ipv4/af_inet.c).
- ptype_all: 所有协议嗅觉器的列表, netif_receive_skb会向所有ptype_all传递skb.
- ptype_base: 具体的协议处理函数的列表.
- net_device的ptype_all: 设备特有的针对所有packet的处理函数.
- net_device的ptype_specific: 设备特有的针对特定协议的处理函数.

# 三 传输层:
## (1)协议函数的注册:
- 传输层协议通过**inet_add_protocol**来注册协议处理函数.

## (2)选择协议处理函数:
- net/ipv4/ip_input.c的ip_local_deliver_finish根据协议类型选择协议的handler处理包.

## (3)相关结构:
- struct net_protocol(include/net/protocol): 用来注册协议处理函数, 协议参考: include/linux/in.h中IPPROTO_XXX.
- init_protos[MAX_INET_PROTOS]: 所有传输层协议的net_protocol的集合.
