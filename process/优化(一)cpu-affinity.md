# 一 概述:
## (1)功能：
- 一个进程的CPU affinity决定了该进程可以执行的cpu的集合.
- 在多处理器系统, 设置CPU affinity可用来提高性能.

## (2)优点:
- 分配给某个进程一个特定的CPU, 设置其它进程运行在其它CPU, 可能保证该进程的最大执行速度.
- 限制进程运行在一个cpu, 可避免由于**cache失效**带来的性能损失.

## (3)相关函数和命令:
- **sched_getaffinity**和**sched_setaffinity**: Linux提供强制的处理器绑定机器, 默认情况下掩码所有位都已设置, 即进程可以在系统中所有可用的处理器上执行; 可通过sched_setaffinity设置几个掩码从而强制进程只能在这些处理器上执行.
- **taskset命令**: 获取和设置一个进程的CPU affinity.
- **sched_getcpu**
- **getcpu**