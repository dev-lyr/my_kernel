# 一 概述:
## (1)功能:
- eventfd: 创建一个用于事件通知的文件描述符.

## (2)API:
- int eventfd(unsigned int initval, int flags)
- eventfd2

## (3)使用场景:
- 当pipe只用于发送事件时, 可以使用eventfd代替, eventfd的kernel开销远远小于管道, 并且只需要一个文件描述符.
- 当在内核使用时, eventfd文件描述符可作为内核空间和用户空间的bridge, 例如kernel AIO通知文件描述符一个操作完成.
- 重要一点eventfd可以像其它文件描述符一样, 被select,epoll和poll监控.
