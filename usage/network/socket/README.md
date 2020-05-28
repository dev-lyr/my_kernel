# 一 概述: 
## (1)概述:
- net/socket.c: 定义相关系统调用函数.
- net/ipv4/af_inet.c: inet_stream_ops, inet_dgram_ops, inet_sockraw_ops支持各协议类型支持的socket操作, 结构为struct proto_ops.
- 查询对应实现的逻辑: struct socket->struct proto_ops ->struct sock->struct proto(tcp_proto:net/ipv4/tcp_ipv4.c)

## (2)常用套接字种类:
- TCP套接字.
- UDP套接字.
- Unix域(Local)套接字: 本地客户/服务器通信方式之一.
- 原始套接字.

