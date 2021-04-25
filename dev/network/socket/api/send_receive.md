# 一 概述:
## (1)读写函数种类:
- read和write
- send和recv: 只适用于面向连接的套接字.
- sendto和recvfrom: 适用于面向连接的和无连接的套接字.
- readv和writev
- sendmsg和recvmsg: 适用于面向连接的和无连接的socket.
- 备注: 最上面的其它读写函数都可用sendmsg和recvmsg替换.

# 二 send和recv:
## (1)概述:
- 与read和write函数类似, 多了一个flags参数.
- send只用于处于连接状态的套接字(即接收方是知道的).

## (2)flags:
- MSG_CONFIRM
- MSG_DONTROUTE: 告知内核无需执行路由表查找, 目的地就在本地网络中.
- MSG_DONTWAT: 将单个I/O操作临时指定为非阻塞, 然后执行I/O操作, 然后关闭非阻塞标记.
- MSG_EOR
- MSG_MORE
- MSG_NOSIGNAL
- MSG_OOB: 对于send表明即将发生带外数据; 对于recv表示即将读入的是带外数据不是普通数据.

# 三 sendto和recvfrom:
## (1)概述:
- 主要用于UDP, 但也可用于tcp(此时to和tolen等参数被忽略).


# 四 sendmsg和recvmsg:
## (1)概述:
- 最通用的I/O函数, 可把其它都替换为sendmsg和recvmsg.