# 一 概述:
## (1)概述:
- Linux的调度基于**分时(time sharing)**技术, **可抢(preemptable)占**的策略, **动态优先级**.
- 调度算法需要在两个矛盾的目标中寻找平衡: 响应时间短和最大系统利用率(高吞吐量).
- 调度算法根据进程是普通进程还是实时进程而不同.
- 进程可分为: I/O密集型和CPU密集型.
- Linux调度器以模块的形式提供, 目的允许不同类型的进程可以选择针对性的调度策略.
- 系统中每个cpu都有自己的运行队列(就绪队列), 系统中每个可运行进程属于且只属于一个可运行队列, 并且只能在该运行队列的CPU上执行.
- Linux每个cpu都有一个swapped/idle进程(id为0), cpu空闲时候会去唤醒该进程.

## (2)调度策略(policy):
- **实时进程(real-time process)**: SCHED_FIFO, SCHED_RR(默认)和SCHED_DEADLINE.
- **普通进程(normal process)**: SCHED_NORMAL(也称SCHED_OTHRE, 默认Linux分时调度)和SCHED_BATCH.
- **SCHED_IDLE**: 调度优先级很低的进程, 进程的静态优先级为0.
- 备注: SCHED_NORMAL和SCHED_BATCH和SCHED_IDLE对应调度器类cfs; SCHED_FIFO和SCHED_RR对象调度器类rt; SCHED_DEADLINE对应dt.

## (3)进程描述符相关字段:
- int prio: 进程动态优先级, **调度器使用的是这个字段**, 通过effective_prio计算出.
- int normal_prio: 进程动态优先级, 基于进程的静态优先级和调度策略(实时进程或常规进程)计算出来.
- int static_prio: 进程静态优先级, 在进程启动时分配, 可通过nice和sched_setscheduler系统调用修改.
- unsigned long rt_priority: 进程实时优先级, 范围0-99, 越小优先级越高.
- unsigned int policy: 调度策略.
- sched_class
- sched_entity

## (4)相关系统调用:
- nice和renice和setpriority: 设置nice值(-19-20), 即设置静态优先级.
- chrt: 设置一个进程的实时属性.
- sched_getscheduler和sched_setscheduler: 获取和设置**进程**的调度策略.
- sched_setparam和sched_getparam: 设置和获取进程的实时优先级.
- sched_rr_get_interval: 获取进程时间片值.
- sched_getaffinity和sched_setaffinity: Linux提供强制的处理器绑定机器, 默认情况下掩码所有位都已设置, 即进程可以在系统中所有可用的处理器上执行; 可通过sched_setaffinity设置几个掩码从而强制进程只能在这些处理器上执行.
- sched_yeild: 暂时让出处理器.
- sched_getcpu/getcpu

## (5)抢占时机:
- 高优先级进程TASK_RUNNING状态.
- 时间片到期.

## (6)备注:
- Documentation/scheduler
- kernel/sched
- include/uapi/linux/sched.h
- include/linux/sched.h

# 二 普通进程的调度:
## (1)概述:
- 普通进程有两个优先级: 静态优先级(决定时间片的长短)和动态优先级(调度程序选择执行进程的依据).
- 备注: 完全公平调度CFS, kernel/sched/fair.c,Documentation/scheduler/sched-design-CFS.txt.

## (2)SCHED_NORMAL

## (3)SCHED_BATCH

# 三 实时进程的调度
## (1)概述:
- Linux为实时进程提供两种调度策略: SCHED_FIFO, SCHED_RR和SCHED_DEADLINE.
- SCHED_FIFO和SCHED_RR都是静态优先级, 内核不为实时进程计算动态优先级, 这样保证高优先级的实时进程总能抢占优先级低的进程.
- 代码: kernel/sched/rt.c和kernel/sched/deadline.c.

## (2)SCHED_FIFO:
- 先入先出调度算法, 不使用时间片, 一旦处于可执行状态, 就会一直执行下去, 直至阻塞或显式让出CPU.
- 只有较高优先级的SCHED_FIFO或SCHED_RR进程才能抢占SCHED_FIFO进程, 若同优先级, 则在进程愿意让出CPU时会轮流执行.
- SCHED_FIFO进程执行会比任何SCHED_NORMAL进程都优先得到调度.

## (3)SCHED_RR:
- 与SCHED_FIFO类似, 是带有时间片的SCHED_FIFO, 当SCHED_RR进程执行完它的时间片, 同一优先级的其它实时进程会被轮流调度.
- 低优先级的SCHED_RR进程不能抢占高优先的, 即使时间片耗尽.

## (4)SCHED_DEADLINE

# 四 优先级:
## (1)概述:
- 内核使用0-139来表示内部优先级, 值越低优先级越高, 其中0-99由实时进程使用, 100-139(nice的值-20到19)由普通进程使用.
- 用户空间可以通过nice命令设置进程的静态优先级, nice值范围是-20到19.

## (2)普通进程:
- 静态优先级: 值越大优先级越低, 静态优先级决定了进程基本时间片的长度, 可通过nice和setpriority改变.
- 动态优先级: 值越大优先级越低, 动态优先级是调度程序选择新进场来运行时的依据.
- 备注: 新进程总是继承父进程的静态优先级.

## (3)实时进程:
- 实时优先级: 可通过sched_setparam和sched_setscheduler来改变.

## (4)prio字段:
- **调度器使用的是这个字段**, 通过effective_prio计算出.

## (5)normal_prio:
- normal_prio计算出, 不同类型进程计算结果不一样.

## (6)static_prio:
- 进程静态优先级, 在进程启动时分配, 可通过nice和sched_setscheduler系统调用修改.

# 五 时间片:
## (1)概述:
- 时间片大小是进程级别的, 针对每个进程计算时间片.
- 时间片长短对系统性能影响很大, 太长或者太短都不行.
- 若太短,例如和进程切换接近, 则会导致CPU一半时间花费在进程切换上. 
- 若太长,当出现两个进程优先级相同的场景, 会导致延迟比较大.

# 六 运行队列:
## (1)概述:
- 每个cpu有自己的运行队列, 存在放per-cpu变量中, 系统的所有运行队列都在runqueues数组.
- 文件: include/uapi/linux/sched.h, struct rq.

## (2)相关函数:
- this_rq
- cpu_rq

## (3)通用属性:
- lock 
- load
- cpu_load
- nr_running: 运行队列上可运行进程数量, 不考虑优先级和调度类.
- curr: 指向当前运行进程的task_struct.
- idle: 指向idle进程的task_struct.
- nr_switches
- nr_load_updates
- struct cfs_rq cfs: cfs调取器的就绪队列.
- struct rt_rq rt: 实时调度器的就绪队列.
- struct dl_rq dl

## (4)smp相关

# 六 其它结构:
## (1)概述:
- sched_class: fair_sched_class,rt_sched_class等, 是task_struct的属性.
- sched_entity: 调度实体,调度器操作的对象,进程task_struct都有一个调度实体, 因此每个进程都是一个调度实体.
- sched_domain: 调度域.

## (2)sched_class:

## (3)sched_entity:

## (4)sched_domain:
