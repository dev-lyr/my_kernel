# 一 概述:
## (1)功能:
- Linux内核中每种网络设备(真实设备(如NIC)或虚拟设备(Bonding或VLAN))都用这个数据结构表示, 包括软硬件配置信息等.
- 详见include/linux/netdevice.h.

## (2)常用字段:
- const struct net_device_ops * netdev_ops: 定义一些callback指针, 例如:发送包时候调用xxx.

# 二 struct net_device_ops:
## (1)ndo_start_xmit:
- 当package需要传输时调用的函数.

# 三 enum net_device_flags:
## (1)功能:
- 网络设备的flags.
- include/uapi/linux/if.h

## (2)常用flag:
- UP: 接口是打开的, 只对驱动可用, 当接口是active并且准备传输包时内核打开该flag.
- RUNNING: 接口是up和running的, 和up区别:拔掉网线时是up不是running.
- BROADCASE: 广播地址合法.
- MASTER: 负载平衡的master.
- SLAVE: 负载平衡的slave.
- MULTICASE: 支持多播.
- PROMOSC: 混杂模式, 接收所有包.
- LOOPBACK: 一个loopback网络设备.
