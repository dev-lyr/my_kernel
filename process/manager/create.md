# 一 概述:
## (1)概述.
- 父子进程可以共享程序代码(正文)的页，但是要有各自的数据拷贝(堆和栈).
- 一个进程的所有信息对该进程的线程都是共享的，包括：可执行程序的代码、程序的全局内存和堆内存、栈以及文件描述符.
- 每个线程包含执行环境所必需的信息，包括：线程ID，一组寄存器值，栈，调度优先级和策略、信号屏蔽字、errno变量以及线程私有数据.

## (2)写时复制(copy-on-write):
- linux下创建进程采取写时复制技术, 父子进程以只读方式共享相同的物理页,内核只有在有需要写入的时候数据才会被复制一个新的物理页, 在fork之后直接调用exec情况下就不需复制了.
- fork()函数只需为子进程创建一个进程描述符结构，并复制父进程的页表(page table).

## (3)创建方法:
- fork(),vfork()和clone库函数根据各自需要的参数标志调用`_do_fork()`来完成大部分创建工作(kernel/fork.c).

## (4)进程组

## (5)线程组:
- 线程组中多个线程共享同一个PID, 在内部该PID也被称为线程组ID(TGID), getpid返回调用者的TGID, 线程组里的线程可以线程ID(TID)来区分, gettid返回.

## (6)相关:
- execve

# 二 clone:
## (1)功能:
- 用来创建子进程.
- 与fork类似, 不同的是clone允许子进程共享调用进程(即父进程)的部分执行上下文, 例如: 虚拟地址空间, 文件描述符表和信号处理表等.
- clone可以用来实现线程: 在一个程序中多个控制流在一个共享的地址空间中执行.
- clone: _do_fork(clone_flags, ...)

## (2)相关clone flags:
- **CLONE_PARENT** : 若设置, 则新进程的父进程是调用进程的父进程; 若不设置, 则新建进程的父进程为调用进程.
- **CLONE_FS** : 若设置, 则调用进程和子进程共享同一文件系统相关信息, 包括文件系统的root, 当前工作目录, umask, 任何chroot,chdir和umask调用都会影响其它进程; 若未设置, 则子进程copy调用进程的文件系统相关信息.
- **CLONE_FILES** : 若设置, 则调用进程和新进程共享文件描述符表, 任何被调用进程和新进程创建的文件描述符对其它进程都是可用的, 关闭和修改文件描述符对其它进程也受影响; 若不设置, 则新进程copy调用进程的所有打开的文件描述符, 修改文件描述符对其它进程无影响.
- **CLONE_NEWNS** : 所有进程都活在namespace里, 若不设置, 则子进程和父进程存在于同一namespace; 若设置, 则cloned进程在新的namespace; 若设置, 则cloned进程在新的namespace里, 以父进程的namespace副本初始化.
- **CLONE_SIGHAND** : 若设置, 则子进程和父进程共享信号handler表, 调用sigaction改变相关信号的handler则会影响所有进程; 若不设置, 则子进程copy信号的handler表.
- **CLONE_VFORK** : 若设置, 则调用进程被暂停(suspended)直至子进程通过execve或退出释放虚拟地址空间; 若不设置, 则子进程和调用进程都会被调度执行, 任意顺序.
- **CLONE_VM** : 若设置, 则子进程和调用进程在同一内存空间执行, 内存的写对其它进程都是可见的, 并且任何内存mapping和unmapping都会影响其它进程; 若不设置,则子进程在一个独立的调用进程的内存空间副本中执行.
- **CLONE_THREAD** : 若设置, 则子进程和调用进程在同一线程组, 线程组用来支持POSIX线程中多个线程共享同一个PID, 在内部该PID也被称为线程组ID(TGID), getpid返回调用者的TGID, 线程组里的线程可以线程ID(TID)来区分, gettid返回; 若不设置, 则新建线程在一个新的线程组里, 线程组的TGID为线程的TID, 且该线程是线程组的领头.
- 参考: include/uapi/linux/sched.h.

# 三 fork:
## (1)概述:

## (2)kernel_clone_args参数:
- exit_signal=SIGCHLD


# 四 vfork:
## (1)概述:

## (2)kernel_clone_args参数:
- flags: CLONE_VFORK|CLONE_VM
- exit_signal=SIGCHLD

## (3)备注:
- vfork和fork区别: vfork创建的子进程和父进程共享相同的内存地址空间, 不用复制父进程的页表(page table), 但父进程会一直阻塞直至子进程退出(exit)或执行一个新的程序(exec)为止, vfork用在性能敏感且子进程会立即调用exec的应用中.


# 五 pthread_create:
## (1)语法:
- ARCH_CLONE(...)
- clone_flags: CLONE_VM|CLONE_FS|CLONE_FILES|CLONE_SYSVSEM|CLONE_SIGHAND|CLONE_THREAD|CLONE_SETTLS|CLONE_PARENT_SETTID|CLONE_CHILD_CLEARTID|0

## (2)备注:
- glibc/nptl

# 六 内核线程创建(kernel_thread):
## (1)语法:
- _do_fork(flags|CLONE_VM|CLONE_UNTRACED, ...).
