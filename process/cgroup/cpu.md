# 一 概述:
## (1)cpuset子系统:
- 给cgroup中的task分配cpus(在多核系统)和memory node.

## (2)cpu子系统:
- The cpu subsystem **schedules** CPU access to cgroups. 

## (3)cpuacct子系统:
- 生成cgroup中task使用的cpu资源的统计, 包含子groups中的tasks.

# 二 cpuset:
## (1)cpuset.cpus(强制):
- 指定group中tasks可以访问的cpus.
- 格式:逗号分隔列表,-表示范围; 例如:0-2,16,表示cpu0,1,2和16.

## (2)cpuset.cpu_exclusive:
- contains a flag (0 or 1) that specifies whether cpusets **other than this one and its parents and children** can share the CPUs specified for this cpuset. 
- 默认为0: CPUs are not allocated exclusively to one cpuset.

## (3)cpuset.mems
- cpuset.mems: list of Memory Nodes in that cpuset

## (4)其它:
- cpuset.memory_migrate flag: if set, move pages to cpusets nodes
- cpuset.mem_exclusive flag: is memory placement exclusive?
- cpuset.mem_hardwall flag:  is memory allocation hardwalled
- cpuset.memory_pressure: measure of how much paging pressure in cpuset
- cpuset.memory_spread_page flag: if set, spread page cache evenly on allowed nodes
- cpuset.memory_spread_slab flag: if set, spread slab cache evenly on allowed nodes
- cpuset.sched_load_balance flag: if set, load balance within CPUs on that cpuset
- cpuset.sched_relax_domain_level: the searching range when migrating tasks

# 三 cpu:
## (1)cfs_period_us和cfs_quota_us:
- cpu.cfs_period_us: specifies a period of time in microseconds (µs, represented here as "us") for how regularly a cgroup's access to CPU resources should be reallocated.
- cpu.cfs_quota_us: specifies the total amount of time in microseconds (µs, represented here as "us") for which all tasks in a cgroup can run during one period.

## (2)shares:
- cpu.shares: 一个整数值, 指定cgroup中tasks的可用cpu时间的相对比例, 若2个不通cgroup中的task有相同的share值则

## (3)stat:
- cpu.stat: reports CPU time statistics.

## (4)RT相关control文件:
- cpu.rt_period_us
- cpu.rt_runtime_us

# 四 cpuacct:
## (1)cpuacct.usage:
- 统计cgroup中所有tasks(包括子cgroup中的task)使用的全部CPU时间, 单位为纳秒.

## (2)cpuacct.stat:
- 统计cgroup中所有tasks(包括子cgroup中的task)使用的用户CPU时间和系统CPU时间, 单位USER_HZ变量的定义.

## (3)cpuacct.usage_percpu:
- 统计cgroup中所有tasks(包括子cgroup中的task)在每个cpu的使用时间, 单位为纳秒.
