# 一 概述:
## (1)概述:
- 使用time-ordered红黑树来构建一个未来任务执行的timeline, 所有进程通过p->se.vruntime进行排序.

## (2)实现策略(三种):
- SCHED_NORMAL
- SCHED_BATCH
- SCHED_IDLE

## (3)备注:
- Documentation/scheduler/sched-design-CFS.txt
- Documentation/scheduler/sched-bwc.txt

# 二 相关结构:
## (1)概述:
- cfs_rq: runqueue中cfs相关属性.
- fair_sched_class: 调度类所有方法.

## (2)cfs_rq:

## (3)fair_sched_class

# 三 fair_sched_class

# 四 组调度:
## (1)概述:
- 通常cfs是针对单个task进行调度并且争取在每个task间公平分配cpu.
- 有时需要对包含多个task的task组间提供公平调度, 例如: 为每个用户提供公平调度, 每个用户的多个task属于一个task组.

## (2)相关选项:
- CONFIG_CGROUP_SCHED
- CONFIG_FAUR_CGROUP_SCHED: 允许对CFS任务进行分组, 若该选项被定义则会为每个任务组在cgroup文件系统中创建一个cpu.shares文件.
- 备注: 上面选项需要配置CONFIG_CGROUPS, 并让管理员通过cgroup伪文件系统来创建task组.

## (3)使用:
- cpu.shares文件.
