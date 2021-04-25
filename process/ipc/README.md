# 一 概述：
## (1)IPC(interprocess communication):
- 消息传递
- 同步

## (2)种类:
- 消息传递(管道、FIFO、消息队列)
- 同步(互斥锁、条件变量、读写锁、信号量, 文件锁)
- 共享内存区(匿名共享内存区、有名共享内存区)
- 分布式进程通信: 套接字, MPI, 过程调用(Sun RPC和Java RMI), 间接通信(消息队列, 发布/订阅系统等), 多播和面向流通信等.

## (3)IPC对象的持续性:
- 随进程持续(process-persistent): 一直打开到打开着IPC对象的最后一个进程关闭该对象为止, 例如: 管道和FIFO.
- 随内核持续性(kernel-persistent): 一直存在到内核重新自举和显式删除IPC对象为止, 例如: Posix消息队列、信号量和共享内存区必须至少是随内核持续的，也可是随文件系统持续的，具体取决于实现.
- 随文件系统持续性(filesystem-persistent): IPC对象一直存在到显式删除该对象为止, 例如: 使用映射文件实现的Posix消息队列、信号量和共享内存区.

## (4)相关命令:
- ipcs
- ipcrm
- ipcmk

## (5)备注:
- eventfd

# 二 管道:
## (1)API:
- pipe: 创建一个管道, 一个可以用于进程通信的单向(undirectional)数据通道.
- mkfifo: 创建一个FIFO文件(命名管道).

## (2)pipe和fifo区别

## (3)备注:
- man 7 pipe
- man 7 fifo

# 三 消息队列:
## (1)概述:
- Posix消息队列允许进程以队列形式交换数据.

## (2)Posix API:
- mq_open
- mq_send
- mq_receive
- mq_close
- mq_unlink
- mq_getattr
- mq_notify

## (3)消息队列文件系统:
- 在linux中消息队列在一个虚拟文件系统(类型为mqueue)中创建, 文件系统可以通过以下命令挂载: `mkdir /dev/mqueue; mount -t mqueue none /dev/mqueue`.
- 当文件系统被挂载后, 系统中的消息队列可以被看到并且可以使用常用的文件命令来操作(例如:ls,rm等).

## (4)备注:
- man mq_overview

# 四 共享内存:
## (1)功能:
- 共享内存区是最快IPC方式, 内存区映射到进程的地址空间后, **进程间数据的传输不再涉及内核**. 
- **不需要执行系统调用(不需要在用户态和内核态间copy)**来彼此传递数据; 但是向共享内存区写入和读取信息需要**同步**.

## (2)类型:
- 使用内存映射文件(memory-mapped file): open函数打开一个文件, 然后mmap函数将fd映射到当前进程的地址空间, 对有亲缘或无亲缘关系的进程都适用.
- 匿名内存映射(anonymous memory mapping): 避免创建和打开文件, 用来提供父子进程间的内存共享.
- 共享内存区对象(shared-memory object): shm_open打开一个posix IPC对象,返回的描述符由mmap函数映射到当前进程的地址空间.

## (3)相关函数:
- mmap, munmap: map or unmap files or devices into memory.
- msync: synchronize a file with a memory map.
- shm_open/shm_ulink: Create/open or unlink POSIX shared memory objects.
- shmget: allocates a System V shared memory segment.

## (4)备注:
- /proc/pid/maps
