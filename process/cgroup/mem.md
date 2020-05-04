# 一 概述:
## (1)子系统:
- memory: 生成cgroup中tasks使用的内存资源的统计, 并设置这些task使用的内存limit.
- hugetlb: HugeTLB控制器用来限制每个cgroup的HugeTLB使用量.

## (2)备注:
- https://www.kernel.org/doc/Documentation/cgroup-v1/memory.txt

# 二 memory控制文件:
## (1)memory.stat:
- cache
- rss
- 等等.

## (2)limit相关:
- memory.limit_in_bytes: 设置用户内存(包括文件cache)的最大使用量.
- memory.memsw.limit_in_bytes: 设置内存和swap最大使用量.
- memory.failcnt
- memory.memsw.failcnt

## (3)memory.oom_control:
- 0/1: 开启或者关闭一个cgroup的oom kill.
- 0表示开启, 默认是开启.

# 三 hugetlb控制文件
