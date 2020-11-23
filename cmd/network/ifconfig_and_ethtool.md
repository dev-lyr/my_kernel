# 一 ifconfig:
## (1)功能:
- 配置运行在内核里的网络接口, 包括: up和down, 配置ip和掩码, 查询网卡状态和流量等等.

## (2)语法:
- ifconfig [interface]
- ifconfig interface [aftype] options | address

## (3)选项:
- up/down: 激活/关闭某接口.
- [-]arp: 开启或关闭在接口使用arp协议, 若是关闭, 会显示NOARP.
- [-]promisc: 开启或关闭接口的混杂模式, 若开启, 会显示PROMISC, 且所有网络上的包会被该接口接收.
- [-]allmulti: 开启或关闭多播模式, 若开启, 会显示MULTICASE, 所有多播的包会被该接口接收.
- [-]broadcase [adr]: 若addr指定则设置该接口的广播地址; 否则, 则是设置或清除网卡的IFF_BROADCASE标记.
- mtu N: 设置最大传输单元.
- netmask addr: 设置掩码.
- address: 分配给该接口的ip地址.

## (4)输出:
- 连接类型:以太网(ethernet) HWaddr:硬件地址
- 网卡的IP地址, 广播地址和掩码.
- 网卡的状态: UP(网卡开启状态), RUNNING(网卡网线连接上), BROADCAST(支持广播), MTU等等.
- 接收包的统计(RX)
- 发出包的统计(TX)
- 接收和发出包的字符统计.

## (5)RX和TX字段:
- errors
- dropped
- overruns
- frame
- collisions
- exqueuelen

## (6)网卡状态:
- UP/DONW
- RUNNING
- BROADCAST
- MTU

## (7)备注:
- 接收和发出包的统计: /proc/net/dev.

# 二 ethool:
## (1)功能:
- 查询和修改以太网卡的配置.

## (2)常用:
- ethtool xxx: 查询网卡的相关配置.
- ethtool -i xxx: 查询网卡的驱动的相关信息.
- ethtool -k/-K: 查询和修改网卡offload配置.
- ethtool -s/--change xxx: 修改网卡的配置.
- ethtool -S/--statistics
