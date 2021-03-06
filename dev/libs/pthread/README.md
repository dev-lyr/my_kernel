# 一 线程:
## (1)概述:
- 线程在进程内执行环境必需的信息: 线程ID、一组寄存器值、栈、调度优先级和策略、信号屏蔽字、errno变量以及线程私有数据.
- 一组并发线程运行在一个进程的上下文中, 每个线程都有自己独立的线程上下文: 线程ID、栈、栈指针、程序计数器、条件码和通用目的的寄存器值.每个线程和和其它线程共享进程上下文的剩余部分: 整个用户虚拟地址空间(代码、读/写数据、堆、已经所有共享库代码和数据区), 也共享同样的打开文件集合.
- Pthreads引入了一种全新的报错方式: Pthreads中的函数通过返回值表示错误状态, 而没有使用errno变量.
- Pthreads在提供了一个在线程内的errno变量, 只是为了和使用errno的现有函数兼容.每个线程都有属于自己的局部errno以避免一个线程干扰另一个线程.

## (2)线程标识:
- 线程ID: 线程ID只在它所属的进程环境中有效和唯一, 进程ID在整个系统唯一; 线程ID的类型为pthread_t, 可移植的操作系统实现不能把它作为整数.
- 相关函数: pthread_self():获取线程ID, 返回调用线程的线程ID; pthread_equal(pthread_t tid1, pthread_t tid2): 比较两个线程ID是否一样.

## (3)线程状态

## (4)线程组

## (5)备注:
- 编译和链接时需-lpthread.

# 二 线程创建:
## (1)pthread_create:
- tid: tid指向的内存单元被设置为新创建线程的线程ID.
- attr: 用来定制各种不同的线程属性.(不定制时, 设置为NULL)
- start_routine: 新创建的线程从start_routine函数的地址开始运行, 还函数只有一个无类型指针参数arg.

## (2)分离状态:
- pthread_detach(使线程进入分离状态): 默认情况下, 线程的终止状态会保存到对该线程调用**pthread_join**, 如果线程已经处于分离状态, 线程的底层存储资源可以在线程终止时就立即释放.
- pthread_attr_setdetachstate: 设置线程属性detachstate.
- detachstate: PTHREAD_CTREATE_DETACH(分离状态启动)或PTHREAD_CREATE_JOINABLE(正常状态启动).
- pthread_attr_getdetachstate: 获取当前的线程属性detachstate.

## (3)备注:
- linux中使用clone系统调用来实现pthread_create.
- clone系统调用创建子进程, 这个子进程可以共享父进程一定数量的执行环境, 这个数量是可配置的.

# 三 线程终止:
## (1)方式:
- 线程从启动例程返回, 返回值是线程的退出码.
- 线程可以被同一进程的其他线程取消(pthread_cancel).
- 线程调用pthread_exit.
- 主线程从main函数返回(或者return)时会终止子线程(Java不会), 若主线程调用pthread_exit()终止的话则不会终止子线程.
- 注意: 如果进程中任意函数调用exit、_exit或_Exit, 那么整个进程就会终止.

## (2)相关函数:
- void pthread_exit: 终止调用线程, 并返回retval作为线程的返回值, 其他同进程中的线程可以用pthread_join函数访问到这个指针.如果对线程返回值不感兴趣, 则可以把retval设为NULL, 这样pthread_join只等待指定线程终止, 不获取线程的终止状态.
- pthread_join: 调用线程一直阻塞, 等待thread指定的线程终止, thread指定的线程必须是joinable的.
- pthread_cancel: 发送一个取消请求给线程tid, 是否或何时目标线程对取消请求响应取决于线程的两个属性: 可取消状态和可取消类型.
- pthread_cancel不等待线程终止, 在默认情况下, 线程在取消请求发出以后继续运行, 直到线程到达某个取消点.取消点: 线程检查是否被取消并按照请求进行动作的一个位置.某些函数在调用时, 取消点都会出现, 也可以调用pthread_testcancel自己添加取消点.

## (3)线程清理处理程序:
- void pthread_cleanup_push.
- void pthread_cleanup_pop: 如果参数execute为0, pthread_cleanup_pop只删除上一个清理函数, 而不执行.
- 线程可以建立多个处理程序, 处理程序记录在栈中, 所以执行顺序与注册顺序相反.
- 线程执行以下动作时, 会调用清理函数: 调用pthread_exit; 响应取消请求;用非0参数执行pthread_cleanup_pop.
- 备注: 线程从启动例程返回而终止的话, 不调用线程清理处理程序; pthread_cleanup_push与pthread_cleanup_pop必须成对出现, 否则编译不通过.
