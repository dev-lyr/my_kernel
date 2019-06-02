# 一 概述:
## (1)概述:
- 用于linux各子系统间事件感知, 采用的是发布/订阅模型.
- 接收者(notified): 要求接收某事件的子系统, 会提供回调函数用于执行.
- 通知者(notifier).

## (2)通知链的类型:
- Atomic notifier chains: callback在中断/原子上下文中执行, 不允许block.
- Block notifier chains: callback在进程上下文中执行, 可以block.
- Raw notifier chains: 对callback, 注册和取消注册都没有限制, 所有的锁和保护由caller提供.
- SRCU notifier chains: Block notifier chains的变种, 同样的限制.

## (3)备注:
- 代码: include/linux/notifier.h和kernel/notifier.c.