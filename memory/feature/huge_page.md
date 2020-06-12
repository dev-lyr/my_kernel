# 一 概述:
## (1)背景:
- X86 cpus通常支持4K和2M的页大小, ia64支持更多页大小:4K,8K...16M等.
- TLB: 是存放虚拟地址到物理地址映射的cache, 是处理器上的稀缺资源, 操作系统应该充分利用.

## (2)备注:
- kernel编译时需指定CONFIG_HUGETLBFS和CONFIG_HUGETLB_PAGE选项.
- 用户可以使用mmap系统调用或shmget和shmat来使用大页.
- /Documentation/vm/hugetlbpage.txt
- hugetlbfs: https://github.com/libhugetlbfs/libhugetlbfs

# 二 操作:
## (1)/proc/meminfo:
- HugePages_Total: 大页pool的大小.
- HugePages_Free: 大页池中没有分配的大页数量.
- HugePages_Rsvd: 预留但未分配.
- HugePages_Surp.
- Hugepagesize.
