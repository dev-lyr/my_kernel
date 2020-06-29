# 一 概述:
## (1)概述:
- Data Plane Development Kit(DPDK): 由多个用来加速包处理的库组成, 可以运行在多种cpu架构上.

## (2)特点:
- 使用轮询代替中断.
- 通过huge page,减少tlb cache miss.
- 使用cpu亲和性
- UIO(UserSpace I/O)

## (3)备注:
http://dpdk.org/
