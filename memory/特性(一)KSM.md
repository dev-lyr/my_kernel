# 一 概述:
## (1)概述:
- KSM(Kernel Samepage Merging): 一种针对重复(de-duplication)的内存节约特性, 通过共享的相同的内存来节约内存, 利用COW(copy on write)机制.
- KSM最初被KVM使用, 用来让更多虚拟机通过共享公共数据的方式来节约内存, 从而可以运行更多虚拟机(内存超用); 但是可扩展到任何会产生多份相同数据的应用.
- KSM只会merge匿名页, 而不是file cache.

## (2)ksmd:
- ksmd守护进程: 定期扫描向它注册的用户的内存区域, 寻找可以被单个写保护(当有进程需要写时候自动copy一份当前的页)的页代替的有一致内容的多个页.

## (3)备注:
- Documentation/vm/ksm.txt