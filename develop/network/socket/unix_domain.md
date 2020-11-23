# 一概述:
## (1)功能:
- Unix域提供两类套接字: 字节流套接字(类似tcp)和数据包套接字(类似udp).
- Unix域套接字可以是**无名的**或者绑定到一个**文件系统路径名**.
- Unix域协议不是一个实际的协议族, 而是单机客户/服务器通信方式之一, 属于IPC的一种.
- Unix域中表示client和server的协议地址是普通文件系统中的路径名.

## (2)优点:
- Unix域套接字比同一机器的TCP/UDP套接字**性能好**.
- Unix域套接字可以在同一主机上的不同进程(无亲缘关系)间传递描述符.
- Unix域套接字可以把client的凭证(用户ID和组ID)提供给服务端, 从而提高额外的安全检查.

## (3)使用:
- unix_socket = **socket**(AF_UNIX, type, 0);
- error = **socketpair**(AF_UNIX, type, 0, int *sv);
- type: SOCK_STREAM和SOCK_DGRAM.

## (4)备注:
- man 7 unix
