# 一 概述:
## (1)概述:
- 功能: 将进程**虚拟地址空间**映射到**物理地址空间**.
- 每个进程有自己的页表.

# 二 多级分页:
## (1)概述:
- 由于虚拟地址空间大部分区域没有使用, 也就是没有关联到页框, 因此需要使用**多级分页**.
- linux采用**四级页表**, 以下以linux为例.
- 采用多级页表缺点: 每次必须访问多个数组才能将虚拟地址转换为物理地址; cpu通过**TLB**和**内存管理单元(MMU)**来优化内存访问操作.

## (2)虚拟地址组成(分割为5部分):
- 全局页目录(Page Global Directory, PGD): 包含一些PUD的地址.
- Page Upper Directory(PUD): 包含一些PMD的地址.
- 中间页目录(Page Middle Directory, PMD): 包含一些Page Table的地址.
- Page Table: 每个page table entry(PTE)指向一个page frame.
- OFFSET: 指定页内部一个字节位置.
- 备注: 每部分的bit数依赖计算机架构.

## (3)macros:
- PGDIR_SHIFT
- PUD_SHIFT
- PMD_SHIFT
- PAGE_SHIFT: 指定OFFSET属性的长度.
- 等等.

## (4)备注:
- 页表是根据VPN(virutal page number)索引来查找, 因此即使没有使用到的page也会占用一个entry, 所以单级页表会占用很多内存.
