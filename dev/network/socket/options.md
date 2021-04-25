# 一 获取和设置套接字选项的函数：
## (1)getsockopt和setsockopt:
- `int getsockopt(int sockfd，int level，int optname，void *optval，socklen_t *optlen)`
- `int setsockopt(int sockfd，int level，int optname，const void*optval，socklen_t optlen)`
- sockfd：必须指向一个打开的套接字描述符.
- level：或为通用套接字代码(SOL_SOCKET)；或为某个特定于协议的代码(IPPROTO_IP或IPPROTO_TCP等).
- optname：选项名.
- optval：setsockopt从optval取得选项待设置的新值；getsockopt把已获取的当前值放到*optval中.
- optlen：指定optval的大小.
- 备注: 仅适用于套接字.

## (2)fcntl:
- 把套接字设置为非阻塞I/O或其他等.

## (3)ioctl

## (4)备注:
- 选项可能存在于多类协议级别.
- 实现:net/socket.c

# 二 套接字选项：
## (1)按level分类(列出常见四项，还有其它)：
- SOL_SOCKET(通用套接字选项)
- IPPROTO_IP(IPv4套接字选项)
- IPPROTO_IPv6(IPv6套接字选项)
- IPPROTO_TCP(TCP套接字选项)

## (2)常见通用套接字选项：
- SO_BROADCASE: 本选项开启或禁止发送广播消息的能力，只有数据报套接字(UDP)支持广播.
- SO_DEBUG: 仅TCP支持，开启后，内核为TCP在该套接字发送和接收的所有分组保留详细的跟踪信息.
- SO_DONREOUTE: 规定外出的分组将绕过底层协议的正常路由机制.
- SO_ERROR: 通过SO_ERROR选项访问so_error的值.so_error即待处理错误，套接字发生错误时，原来Berkeley的内核将so_error变量设置为标准Unix EXXX值的一个.
- SO_KEEPALIVE: 给一个TCP套接字设置该选项后，如果两小时内任一方向都没有数据交换，TCP就发送一个保活探测分节.
- SO_LINGER: 指定close函数对面向连接协议如何操作.
- SO_OOBINLINE: 带外数据被留在正常的输入队列中.
- SO_RCVBUF和SO_SNDBUF: 改变发送或接收缓冲区的大小.
- SO_RCVLOWAT和SO_SNDLOWAT: 允许修改发送和接收低水位标记(由select等使用), 发送标记表示当发送缓冲区可用空间达到标记时则返回可写, 接收标记表示当接收缓冲区可用空间到达标记时返回可读.
- SO_RCVTIMEO和SO_SNDTIMEO: 给套接字的发送和接受设置一个超时值.
- SO_REUSEADDR和SO_REUSEPORT.
- SO_TYPE: 返回套接字类型，诸如SOCK_STREAM或SOCK_DGRAM.
- SO_USELOOPBACK: 仅适用于路由域套接字.

## (3)TCP套接字选项(man tcp, 前两个是标准, 后面的不可移植)：
- TCP_MAXSEG: 获取或设置TCP连接的最大分片大小.
- TCP_NODELAY: 开启本选项将禁止TCP的Nagle算法, 默认是启动的.
- TCP_QUICKACK: 开启或关闭ack-delay算法.