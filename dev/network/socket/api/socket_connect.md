# 一 socket函数:
## (1)功能:
- 创建用来通信的endpoint, 函数返回一个描述符.
- 格式: int socket(int domain, int type, int protocol).
- domain参数: 指定通信域, 选择用来通信的协议族(protocol family), 在sys/socket.h中定义.
- type: 套接字的类型, 指定通信语义, 协议族并没有实现所有的套接字类型.
- protocol: 指定特定的socket使用的协议, 通常在指定domain和type下只有一个唯一的协议支持, 查看protocols(5)来查询协议名字和num的映射.

## (2)domain类型:
- PF_UNIX(已废弃), PF_LOCAL: 本地通信, Unix套接字.
- PF_INET: IPv4.
- PF_INET6: IPv6.
- PF_PACKET
- PF_NETLINK
- 等等.

## (3)type的类型:
- SOCK_STREAM: 数据流套接字.
- SOCK_DGRAM: 数据报套接字.
- SOCK_SEQPACKET
- SOCK_RAW: 原始套接字.
- SOCK_RDM
- SOCK_PACKET

## (4)protocol:
- 参见/etc/protocols文件.

# 二 connect:
## (1)概述:
- 格式: connect(int sockfd, const struct sockaddr * serv_addr, socklen_t addrlen)
- 功能: 通过socket关联的文件描述符fd来连接serv_addr指定的远方地址.
