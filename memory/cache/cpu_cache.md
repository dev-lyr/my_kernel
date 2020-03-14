# 一 概述:
## (1)概述:
- 现代CPU至少有三个独立的caches: 指令cache(加速可执行指令的获取); 数据cache(加速数据的获取和存储); TLB(加速虚拟地址到物理地址的翻译, 包括可执行执行和数据).
- 数据cache通常是层次结构的, 可分为L1,L2,L3等.
- TLB是内存管理单元的一部分, 并没有直接和CPU cache相关.

## (2)备注:
- https://en.wikipedia.org/wiki/CPU_cache

# 二 多层次缓存
## (1)概述:
- 现代CPU有用多层次的CPU缓存, L1,L2,L3等等.
- L1: 分隔(split)为L1数据缓存和L1指令缓存.
- L2: L2不分隔, 作为分隔的L1的公共缓存, 多核处理器中每个核拥有独立的L2缓存并且通常不与其他核共享.
- L3和更高层次缓存在核间共享并且不分裂.

# 三 cache miss