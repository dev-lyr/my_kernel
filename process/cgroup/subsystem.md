# 一 概述:
## (1)子系统类型:
- cpuset
- cpu
- cpuacct
- memory
- devices
- freezer
- net_cls
- net_prio
- blkio
- perf_event
- hugetlb
- pids

## (2)备注:
- /proc/cgroups
- https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/6/html-single/resource_management_guide/index 

# 二 cpusets:
## (1)功能:
- 给cgroup中的task分配cpus(在多核系统)和memory node.

## (2)相关control文件:
- cpuset.cpus: list of CPUs in that cpuset
- cpuset.mems: list of Memory Nodes in that cpuset
- cpuset.memory_migrate flag: if set, move pages to cpusets nodes
- cpuset.cpu_exclusive flag: is cpu placement exclusive?
- cpuset.mem_exclusive flag: is memory placement exclusive?
- cpuset.mem_hardwall flag:  is memory allocation hardwalled
- cpuset.memory_pressure: measure of how much paging pressure in cpuset
- cpuset.memory_spread_page flag: if set, spread page cache evenly on allowed nodes
- cpuset.memory_spread_slab flag: if set, spread slab cache evenly on allowed nodes
- cpuset.sched_load_balance flag: if set, load balance within CPUs on that cpuset
- cpuset.sched_relax_domain_level: the searching range when migrating tasks

# 三 cpu:
## (1)功能：
- The cpu subsystem **schedules** CPU access to cgroups. 
- Access to CPU resources can be scheduled using two schedulers:: CFS(Completely Fair Scheduler)和RT(Real-Time scheduler).
- **CFS**: a proportional share scheduler which divides the CPU time (CPU bandwidth) proportionately between groups of tasks (cgroups) depending on the **priority/weight of the task or shares assigned to cgroups**.
- **RT**: a proportional share scheduler which divides the CPU time (CPU bandwidth) proportionately between groups of tasks (cgroups) depending on the priority/weight of the task or shares assigned to cgroups.

## (2)CFS相关control文件:
- cpu.cfs_period_us
- cpu.cfs_quota_us
- cpu.stat:reports CPU time statistics.
- cpu.shares: contains an integer value that specifies a relative share of CPU time available to the tasks in a cgroup.

## (3)RT相关control文件:
- cpu.rt_period_us
- cpu.rt_runtime_us

# 四 memory:
## (1)功能:
- 限制cgroup中tasks的内存使用, 并自动产出内存报告.

## (2)相关control文件:
- memory.usage_in_bytes: set/show limit of memory usage.
