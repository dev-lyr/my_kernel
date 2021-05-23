# 一 概述:
## (1)设备和内核交互方式:
- 轮询(内核驱动)
- 中断(设备中断驱动)

## (2)队列:
- 入口队列
- 出口队列

## (3)相关配置:
- /proc/sys/net/core

# 二 轮询:
## (1)概述:
 - 内核不断检查设备是否有事情发生, 例如:内核可以持续读取设备的一个内存的寄存器或定期器到期就去检查该寄存器.

## (2)缺点:
 - 浪费系统资源.

# 三 中断:
## (1)概述:
- 当事件发生时, 设备驱动程序向内核发送硬件中断, 内核将中断其它活动, 执行中断处理函数.
- 接收帧分为两步: 驱动程序将帧拷贝到内核可访问的输入队列; 内核处理帧数据.
- 第一步在中断环境执行, 可以抢占第二步, 在高流量下, 第一步持续抢占第二步, 造成输入队列塞满, 新的帧无法进入队列, 旧的帧又没机会处理(没有CPU可用), 系统就会崩溃.

## (2)优缺点:
- 优点: 帧的接收和处理之间的延时很短.
- 缺点: 每接收一个帧就产生一个硬件中断, 在低流量负载下是最佳选择, 但高流量负载下就会让CPU一直在处理中断事件.

## (3)变种:
- 变种一: 定时器驱动的中断事件(驱动程序会只是设备定期产生一个中断, 处理函数会处理上一次中断到现在的所有帧).
- 变种二: 中断期间处理多帧(通知内核中断事件, 处理函数会持续下载帧并放入内核的输入队列).

# 四 Soft IRQ:
## (1)概述:
- NET_RX_SOFTIRQ: net_rx_action处理入流量.
- NET_TX_SOFTIRQ: net_tx_action处理出流量.
- net/core/dev.c.

## (2)net_rx_action:
- NAPI和非NAPI都是由该函数接收包.
- 非NAPI的poll函数在net_dev_init时初始化为process_backlog.
- NAPI的poll函数由设备驱动程序提供并在初始化时调用netif_napi_add来设置.
- poll函数会调用netif_receive_skb来处理包, 无论是NAPI还是非NAPI设备.

## (3)net_tx_action
- NAPI和非NAPI都用该函数发送包.

# 五 softnet_data(包的接收和发送)
## (1)概述:
- 功能: 进来的包都存放在每个CPU的队列, 每个cpu都有自己的softnet_data.
- 在include/linux/netdevice.h中定义,在net_dev_init中针对每个cpu进行初始化.

## (2)接收字段:
- struct sk_buff_head input_pkt_queue: 非NAPI设备的输入队列.
- struct napi_struct backlog: 非NAPI设备(没有napi_struct结构)使用, poll函数在net_dev_init时初始化为process_backlog.
- struct sk_buff_head process_queue
- struct list_head poll_list: 双向链表, 其中的设备都是带有输入帧等待处理的.

## (3)发送字段:
- output_queue: 输出队列, 其中的设备有数据需要发送.
- completion_queue
