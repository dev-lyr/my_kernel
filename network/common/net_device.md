# 一 概述:
## (1)功能:
- Linux内核中每种网络设备(真实设备(如NIC)或虚拟设备(如:Bonding或VLAN))都用这个数据结构表示, 包括软硬件配置信息等.

## (2)备注:
- 详见include/linux/netdevice.h.

# 二 net_device字段:
## (1)常用:
- ifindex: interface index,唯一的ID,调用dev_new_index注册设备时分配.
- const struct net_device_ops * netdev_ops: 定义一些callback指针.
- netdev_rx_queue
- master: 有些协议允许多个设备集合起来作为单一设备, 例如:bonding, 群组中某个设备会被选择为主设备,作为特殊角色, 该指针指向master的net_device.
- struct net_device_stats stats: 遗留的统计结构体, 使用rtnl_link_stats64替代.

## (2)配置:
- name: 设备名称,例如:eth0.
- type: 接口硬件类型,
- req: 中断编号,可由多个设备共享,驱动程序使用request_irq函数分配此变量,且使用free_irq释放.
- dma: 设备使用的DMA通道(若有).
- flags: 某些位代表网络设备的通能(IFF_MULTICAST),某些表示状态改变(IFF_UP或IFF_RUNNING), 可在include/uapi/linux/if.h发现标识的完整列表.
- priv_flags: 这些flags对用户空间不可见, 只能由驱动程序和内核修改.
- mtu: 最大传输单元,表示设备能处理的最大帧的尺寸.

## (3)接收:
- rx_handler: 接收包的处理函数.
- _rx: 接收队列的数组.
- num_rx_queues: 调用register_netdev时分配的接收队列数量.
- real_num_rx_queues: 当前设备中active的队列数量.

## (4)发送:
- _tx
- tx_queue_len
- num_tx_queues
- real_num_tx_queues

## (5)列表管理:
- net_device会被插入到一个全局list和两个hash表中.
- next
- name_hlist
- index_hlist

## (6)流量管理:

## (7)相关ops:
- net_device_ops
- ethtool_ops

# 三 常用函数:
## (1)netdev_start_xmit:
- 传输帧, 底层调用net_device_ops的ndo_start_xmit.

# 四 struct net_device_ops:
## (1)ndo_start_xmit:
- 当package需要传输时调用的函数.

# 五 enum net_device_flags:
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
