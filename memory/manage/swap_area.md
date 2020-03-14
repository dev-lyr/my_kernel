# 一 概述：
## (1)交换子系统功能：
- 在磁盘上建立交换区(swap area), 用于存放没有**磁盘映像**的页.
- 管理交换区空间, 当需求发生时, 分配和释放页槽(page slot).
- 提供函数从RAM把页换出(swap out)到交换区或从交换区换入(swap in)到RAM中.
- 理由页表项的换出页标识符(Present)跟踪数据在交换区中的位置.


## (2)交换子系统处理的页类型:
- 属于进程匿名线性区(用户态堆栈和堆)的页(anonymous pages).
- 属于进程私有内存映射的脏页.
- 属于IPC共享内存区的页.

## (3)相关配置和命令:
- mkswap, swapon, swapoff等.
- vmstat
- vm.swappiness

## (4)备注:
- 交换是页框回收的一个高级别特性, 要确保进程的所有页框都能被PFRA随意回收, 而不仅仅是有磁盘映像的页, 则必须使用交换.
- 交换可以用来扩展内存地址空间, 使内核可以运行超过系统安装物理内存总量的应用, 性能而言, 对换出页的每一次访问比RAM慢几个数量级别.
- 若性能重要, 则交换仅仅作为最后方案, 增加物理内存才是王道.
- file-backed pages直接和磁盘对应文件交换.

# 二 交换区(swap area):
## (1)概述:
- 从内存换出的页存放在交换区(swap area), 交换区实现可以是磁盘分区或磁盘分区中的文件, 交换区的最大个数由MAX_SWAPFILES宏(默认32)确定.