# 一 概述:
## (1)概述:
- 内核空间进程和用户空间进程的通信方式之一, 是网络应用程序和内核通信的首选方式, iproute2包大部分命令都使用该接口.
- netlink是面向报文的服务, netlink消息由一个包含一个或多个nlmsghdr头部的字节流和相关的负载组成.
- /proc/net/netlink: List of PF_NETLINK sockets.

## (2)备注:
- man 3/7 netlink
- net/netlink
- rfc3549

# 二 用法:
## (1)概述:
- socket(AF_NETLINK, socket_type, netlink_family)
- socket_type: SOCK_RAW和SOCK_DGRAM.

## (2)netlink_family:
- NETLINK_ROUTE: man 7 rtnetlink.
- NETLINK_NETFILTER
- NETLINK_FIREWALL
- NETLINK_INET_DIAG
- NETLINK_SOCK_DIAG
- 等等.
