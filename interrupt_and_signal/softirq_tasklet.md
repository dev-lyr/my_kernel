# 一概述:
## (1)概述:
- 软中断(softirq): 在内核代码中常常表示可延迟函数的所有种类.
- 中断上下文: 表示内核正在执行一个中断处理程序或可延迟函数.
- tasklet: 在软中断基础上实现, 简化了设备驱动程序开发者的工作.
- kernel/softirq.c

## (2)软中断和tasklet区别:
- 软中断: 静态的(在编译时定义); 可以并发在多个CPU上运行(即使同一类型的软中断); 软中断是可重入函数并且明确的使用自旋锁保护其数据结构.
- tasklet: 内核对tasklet的执行进行更加严格控制, 相同类型的tasklet被限制串行执行, 不同类型的tasklet可以在几个cpu上并发执行, tasklet不要求是可重入的.
- 备注: 大部分驱动程序都通过tasklet实现下半部, 网卡是直接使用软中断.
- 备注: tasklet是用软中断HI_SOFTIRQ和TASKLET_SOFTIRQ来实现, 几个tasklet可以与同一软中断相关联.

## (3)软中断类型:
- HI_SOFTIRQ=0: 处理高优先级的tasklet.
- TIMER_SOFTIRQ=1: 和时钟中断相关的tasklet.
- NET_TX_SOFTIRQ=3: 把数据包传送到网卡.
- NET_RX_SOFTIRQ=4: 从网卡接收数据包.
- BLOCK_SOFTIRQ=5: 块I/O操作完成. 参考:block/blk-softirq.c.
- IRQ_POLL_SOFTIRQ=6
- TASKLET_SOFTIRQ=7
- SCHED_SOFTIRQ=8
- HRTIMER_SOFTIRQ=9
- RCU_SOFTIRQ=10
- NR_SOFTIRQS=11
- 备注: linux使用有限个软中断, 应该避免分配新的软中断, 多使用tasklet, 数字越小优先级越高.

## (4)相关数据结构:
- softirq_vec数组: 包含类型为softirq_action的32个元素.

## (5)软中断的执行时机:
- 从一个硬件中断代码处返回.
- 在ksoftirqd内核线程中.
- 显式检查和执行待处理的软中断的代码中, 例如网络子系统.
- 等等.

# 二 相关操作(kernel/softirq.c):
## (1)open_softirq:
- 初始化软中断, 就是将软中断的处理函数根据标号塞入softirq_vec数组.

## (2)raise_softirq:
- 激活软中断, 通常中断处理程序会在返回前激活它的软中断, 使其在稍后被执行. 

## (3)do_softirq:
- 软中断的执行.

# 三 ksoftirqd内核线程:
## (1)概述:
- 每个cpu有自己的ksoftirqd/n内核线性, n表示cpu的逻辑号, 该线程执行run_ksoftirqd()函数.
