# 一概述:
## (1)功能:
- 周期性执行一个任务, 包括刷新磁盘缓存, 交换出不用页框, 维护网络连接等.

## (2)与普通进程区别:
- 内核线程只运行在内核态, 而普通进程可以运行在内核态也可以运行在用户态.
- 内核线程只使用大于PAGE_OFFSET的线性地址.

## (3)备注:
- kernel/kthread.c.
- Documentation/kernel-per-CPU-kthreads.txt
- 可通过grep kthread_run来查找指定的线程.

# 二 相关操作:
## (1)创建:
- kernel_thread: 创建一个内核线程, 底层还是调用do_fork, 在fork.c文件.
- _do_fork(flags|CLONE_VM|CLONE_UNTRACED, ...).

# 三 常见内核线程:
## (1)进程1(init/systemd).

## (2)ksoftirqd/n:
- 每个cpu都有一个ksoftirqd线程, n代表cpu的编号, 详见软中断.

## (3)kswapd:
- 执行内存回收(页框回收).
-  mm/vmscan.c.

## (4)pdflush(centos6后flush):
- 将脏的磁盘高速缓存中的页刷新到磁盘.

## (5) kblockd:
- 执行kblockd_workqueue工作队列中的函数, 周期性激活块设备驱动程序.

## (6)watchdog/n:
- 检测系统中的soft和hard lockup, 每个cpu core一个watchdog线程.
- 相关文件: kernel/watchdog.c, Documentation/lockup-watchdogs.txt.
- 相关配置: kernel.softlockup_panic: 0或1; 对应文件/proc/sys/kernel/softlockup_panic.

## (7)khungtaskd: 
- 检测任务陷入D状态的情况.
- 相关文件: kernel/hung_task.c
- 现象: task xxx blocked for more than n seconds.
- 相关配置:kernel.hung_task_panic: 0(立即操作)或1(直接panic); 对应文件/proc/sys/kernel/hung_task_panic.

## (8)migration:
- 在cpu core之间负载平衡, 每个cpu core都有一个migration线程.
- 相关文件: kernel/stop_machine.c.

## (9)kworker:
- 执行工作队列(workqueue)中的请求.
- 详见中断的工作队列.

