# 一 概述:
## (1)概述:
- Documentation/sysctl/net.txt
- Documentation/networking

# 二 net.core
## (1)somaxconn:
- 设置socket的listen的backlog队列, 当调用listen时指定的backlog大于该值时使用该值.

## (2)netdev_max_backlog(接收端):
- 当网卡接收速度大于cpu的处理速度时, 将package放入cpu的backlog队列, 参见net/dev.c.

## (3)dev_weight:
- 在一个NAPI中断中, kernel可以处理的packets的最大数量, 是一个Per-CPU变量, 默认为64.

## (4)rmem_max和rmem_default和wmem_max和wmem_default:
- rmem_default: 默认的socket的接收buffer的设置, 字节为单位.
- rmem_max: socket的最大接收buffer的设置, 字节为单位.
- wmem_default: 默认的socket的发送buffer的设置, 字节为单位.
- wmem_max: socket的最大发送buffer的设置, 字节为单位.

## (5)optmem_max:
- 每个socket的辅助buffer的最大size, 辅助buffer是一个带有appended data的struct cmsghdr的序列.

# 三 tcp相关(net.ipv4.tcp_*)
## (1)重传(retranmission)相关配置:
- tcp_retries1:默认3, 在已建立的连接上, tcp在不调用网络层的情况下尝试重传连接的次数, 一旦超过该连接, 就会首先当用网络层更新路由, 然后再重传.
- tcp_retries2:默认15, 在已建立的连接上, tcp包的尝试次数, 超过则丢弃该包.
- tcp_syn_retries: 默认6, 不高于127, 内核主动的新建连接发送syn包的尝试次数.
- tcp_synack_retries: 默认5, 不高于255, 内核在被动的连接中, 尝试发送syn ack的次数.

## (2)keepalive相关:
- tcp_keepalive_time: 默认为2小时, 当keepalive开启时, 等待2小时后发送keepalive probe消息.
- tcp_keepalive_probes: 默认为9, 表示决定关闭连接前需发送多少keepalive探测包.
- tcp_keepalive_intvl: 每个keepalive探测包发出的间隔时间, 默认为75s.

## (3)拥塞(congestion)控制相关:
- tcp_congestion_control: 设置新的连接的拥塞控制算法.
- tcp_available_congestion_control: 显示可用的注册的拥塞控制算法.
- tcp_allowed_congestion_control: 显示和设置非特权进程可用的拥塞控制算法.
- tcp_max_ssthresh: 慢启动阈值.
