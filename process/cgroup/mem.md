# 一 概述:
## (1)概述:
- 生成cgroup中tasks使用的内存资源的统计,并设置这些task使用的内存limit.
- 将一组tasks的内存行为与系统其它任务隔离.

## (2)使用场景:
- Isolate an application or a group of applications Memory-hungry applications can be isolated and limited to a smaller amount of memory.
- Create a cgroup with a limited amount of memory; this can be used as a good alternative to booting with mem=XXXX.

## (3)备注:
- https://www.kernel.org/doc/Documentation/cgroup-v1/memory.txt
- mm/memcontrol.c

# 二 memory控制文件:
## (1)memory.stat:
- cache
- rss
- 等等.

## (2)limit相关:
- memory.limit_in_bytes: 设置用户内存(包括文件cache)的最大使用量.
- soft_limit_in_bytes
- memory.memsw.limit_in_bytes: 设置内存和swap最大使用量.
- memory.failcnt
- memory.memsw.failcnt
- memory.swappiness

## (3)oom相关:
- memory.oom_control: 0/1: 开启或者关闭一个cgroup的oom kill, 默认为0, 表示开启.
- cgroup.event_control: an interface for event_fd().

## (4)kmem相关
