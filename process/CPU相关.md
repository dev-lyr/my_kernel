# 一 概述:
## (1)性能指标:
- 主频(clock rate)
- 时钟周期: 1/主频.
- 机器周期: 完成一个基本操作所需要的时间称为机器周期, 例如:取指令等.
- 指令周期(Instruction Cycle): 也称fetch-decode-execute周期, a computer retrieves a program instruction from its memory, determines what actions the instruction describes, and then carries out those actions.
- CPI: Cycles per Instruction.

# 二 CPU亲密性(affinity):
## (1)概述:
- CPU Affinity/CPU pinning: 绑定一个进程或线程在一个cpu或几个cpu上执行.
- 优点: 充分利用cpu cache, 减少性能损失.

## (2)相关API:
- sched_setaffinity和sched_getaffinity
- pthread_setaffinity_np和pthread_getaffinity_np

## (3)备注:
- https://en.wikipedia.org/wiki/Processor_affinity

# 三 CPU私有数据:
## (1)概述:
- DEFINE_PER_CPU和DECLARE_PER_CPU: 每个cpu上变量的声明和定义, include/linux/percpu-defs.h.
- 当创建per-CPU变量时, 每个cpu都会有自己的变量副本, 优点是:可以无锁访问该类变量, 并且变量可以放在每个cpu各自的cache中. 

## (2)备注:
- Document/this_cpu_ops.txt
