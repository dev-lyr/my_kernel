# 一 概述:
## (1)正常终止的情况:
- 调用exit、_exit或_Exit退出.
- 从主函数返回,例如main函数.
- 最后一个线程调用pthread_exit或从启动程序返回.

## (2)异常终止情况:
- 调用abort.
- 收到不能处理的信号.
- 最后一个线程对取消做出响应.

## (3)僵尸进程和孤儿进程:
- **僵尸进程**: 子进程终止，但父进程未调用wait来获取子进程的有关信息，造成子进程占用资源未被释放, 一般是代码bug, 可杀死父进程由init来收尸.
- **孤儿进程**: 父进程在子进程之前终止，子进程变为孤儿进程，解决方法: 首先在当前线程组内给子进程找一个父进程，若不行，则让init进程或进程树上是subreaper进程的作为父进程.

## (4)备注:
- 进程正常或异常终止时，内核会向其父进程发送SIGCHLD信号,系统默认为忽略该信号, 应该设置为收到信号后调用wait来避免子进程成为僵尸进程.
- 若父进程结束，其下的处于为僵尸进程的子进程会有init进程替代收尸.
- atexit函数可以注册在进程终止时的一些处理函数.
- 相关代码: kernel/exit.c.
- pthread: https://github.com/dev-lyr/my_pthread/wiki

# 二 do_exit:
## (1)功能:
- 无论终止方式是什么，都需要调用do_exit()来完成大部分资源的释放操作.
- 调用do_exit之后，与进程相关的资源(地址空间、关闭打开的文件描述符)都被释放, 进程处于TASK_ZOMBIE状态. 现在进程占用的资源是: 内核栈、进程描述符(task_struct结构)、thread_info结构.
- 保存进程描述符是为了让系统有办法在进程结束后获得它的信息，父进程获得已终结子进程的信息或通知内核它不关注这些信息后，子进程的task_struct才会被释放.

# 三 wait相关函数:
## (1)功能:
- 当子进程终止时候, 父进程调用wait来让系统释放子进程相关资源.
- wait
- waitpid