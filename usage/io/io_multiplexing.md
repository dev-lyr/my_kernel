# 一 概述:
## (1)种类:
- select/pselect和poll(fs/select.c)
- epoll(fs/eventpoll.c)

## (2)select和poll缺点:
- select支持文件描述符有限制(FD_SETSIZE:1024)；poll没有这个缺陷.
- 需要遍历所有监听的文件描述符,例如:需使用FD_ISSET来遍历所有描述符看是否有事件发生.
- 每次调用select或poll都需要在用户态和内核态拷贝监听的文件描述符.

## (3)epoll优点:
- 没有描述符限制.
- 每次只返回需要处理的文件描述符.
- 文件描述符只用在调用epoll_ctl时在用户空间和内核空间拷贝一次.

## (4)可读事件种类.

## (5)可写事件种类.

# 二 epoll:
## (1)概述:
- 支持套接字, FIFO等, 但不支持普通文件和目录(select和poll支持), epoll_ctl会返回EPERM错误.
- 可结合多线程使用.
- man epoll

## (2)两种工作模式:
- **LT(Level Triggered)**: 默认，支持阻塞和非阻塞fd.
- **ET(Edge Triggered)**: 只支持非阻塞fd，效率更高.

## (3)两种模式比较:
- **LT**: 只要一个套接字缓冲区还有数据未处理,内核就不断通知你,总能epoll_wait中获取这个事件,不用担心事件丢失.优点:编码简单,不容易出现问题. 缺点:效率低.
- **ET**: 套接字缓冲区还是数据未处理时,若没有新事件到来,则无法通过epoll_wait来获取该事件. 优点:效率高,尤其在大并发情况下,会比LT少很多epoll的系统调用;缺点:编程要求高,易出错.

## (4)使用方法:
- epoll_create
- epoll_ctl
- epoll_wait
- 代码: fs/eventpoll.c

# 三 epoll_create:
## (1)原型:
- int epoll_create(int size)
- 功能: 创建一个epoll文件描述符.
- 创建的epoll文件描述符必须调用close函数关闭.

## (2)size参数:
- size并不是限制了epoll能监听的描述符最大数量,只是对内核初始分配数据结构的一个建议.

# 四 epoll_ctl:
## (1)概述:
-  控制epoll_create创建的描述符(epfd);根据op类型,对文件描述符(fd)执行相关操作.

## (2)参数类型:
- epfd: epoll_create返回的.
- op: EPOLL_CTL_ADD，EPOLL_CTL_MOD，EPOLL_CTL_DEL.
- fd: 普通文件描述符.

## (3)events种类(用bit代表):
- EPOLLIN: 可读.
- EPOLLOUT: 可写.
- EPOLLRDHUP
- EPOLLPRI
- EPOLLERR
- EPOLLHUP
- EPOLLLET: 设置为边界触发, 默认为水平触发.
- EPOLLONESHOT

# 五 epoll_wait:
## (1)概述:
- 等待epoll文件描述符上的事件就绪,超时时间为timeout毫秒.

## (2)参数说明:
- events: 指向所有就绪事件(struct epoll_event)的数组.
- maxevents: 每次返回的最大的事件数量.
- timeout: -1表示无限制等待；0表示不等待；正数表示等待多少毫秒.
