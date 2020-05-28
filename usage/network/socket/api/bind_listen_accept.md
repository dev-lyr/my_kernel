# 一 bind:
## (1)概述:
- 格式: bind(int sockfd, const struct sockaddr *my_addr, socklen_t addrlen)
- 功能: 给sockfd绑定一个本地地址my_addr.

## (2)struct sockaddr

## (3)备注:
- INADDR_ANY: 就是0.0.0.0., 通配地址, 让内核去选择IP, 即本机上所有接口都可以. 
- 127.0.0.1: 本机地址.

# 二 listen:
## (1)功能:
- 为了接收连接, socket在创建之后需要调用listen来接收进来的连接和一个队列来限制进来的连接的数量, 之后连接被accept接收走.
- 格式: listen(int sockfd, int backlog).

## (2)backlog:
- 设置已接连队列的长度, 用来限制已连接的socket的数量, 对应内核net.core.somaxconn, 若backlog大于net.core.somaxconn则以somaxconn的配置为准.
- 内核配置tcp_max_syn_backlog: 用来控制未完成连接队列的长度.

# 三 accept:
## (1)功能:
- 格式: int accept(int sockfd, struct sockaddr *addr, socklen_t * addrlen)
- 从已连接队列中取出第一个连接请求, 创建一个新的已连接(connected)套接字, 并返回一个新的文件描述符关联到socket.
- 该函数对listen的sockfd没有影响.

## (2)参数:
- sockfd: 是一个socket, bind和listen后的socket.
- addr: 指向客户端的地址, 传输层.


