# 一 net_rx_action:
## (1)概述:
- NAPI和非NAPI都是由该函数接收包.
- 非NAPI的poll函数在net_dev_init时初始化为process_backlog.
- NAPI的poll函数由设备驱动程序提供并在初始化时调用netif_napi_add来设置.
- poll函数会调用netif_receive_skb来处理包.

# 二 netif_receive_skb:
## (1)功能:
- 把帧的副本传给每个协议分流器, 例如:包嗅觉器(sniffer).
- 把帧的副本传给skb->protocol锁关联的L3协议处理函数.
- 负责此层必须处理的一些功能, 例如桥接(老版本是handle_bridge, 新版本是br_handle_frame, 在接口加入模式时设置在net_device的rx_handler字段).
