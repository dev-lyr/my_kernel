# 一 概述:
## (1)概述:
- CFS bandwidth control is a CONFIG_FAIR_GROUP_SCHED extension which allows the specification of the **maximum CPU bandwidth** available to a group or hierarchy.

## (2)原理:
- 一个group的带宽通过使用**period**和**quota**来指定, 在每个给定的period(microseconds)周期内, 一个group最多只允许消耗quota(microseconds)的cpu时间.
- 若在group超过了限制, 则group内的task会被throttled且不允许执行, 直至下个period到来.

## (3)备注:
- Documentation/scheduler/sched-bwc.txt: 普通进程.
- Documentation/scheduler/sched-rt-group.txt: 实时进程.

# 二 管理:
## (1)概述:
- quota和period通过cgroupfs的cpu子系统管理.

## (2)相关文件:
- cpu.cfs_period_us: 最小值1ms, 最大1s.
- cpu.cfs_quota: 默认-1,无限制, 最小值1ms.
- cpu.stat
