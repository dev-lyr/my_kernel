# 一 概述:
## (1)概述:
- 实现: kernel/sched/core.c.

# 二 schedule
## (1)概述:
- 调用**__schedule**, 核心内容: 选择下一个要执行的任务; 调用context_switch进行切换.

## (2)主要调用场景:
- **显式锁**: mutex, semaphorem, waitqueue等.
- **设置了TIF_NEED_RESCHED标志**: 该flag在中断或用户空间返回路径上会被check, 为了drive任务间的preemption, 会在中断处理函数schedule_tick内被设置.
- **wakeup**: 唤醒不会导致进入schedule, 它只是将任务添加到运行队列. 若新添加到运行队列的任务会抢占当前任务, 则wake会设置TIF_NEED_RESCHED, 在合适时机schedule会被调用.

## (3)调用方:
- io_schedule.
- do_sched_yeild: 让出当前cpu给其它线程, 若没有其它线程允许在当前cpu, 则返回.
- schedule_idle
- do_task_dead
- preempt_schedule

# 三 context_switch:
## (1)功能
- switch to the new MM and the new thread's register state.

## (2)switch_mm:
- switch内存.

## (3)switch_to:
- switch寄存器状态和栈.
