# 一 概述:
## (1)概述:
- 用于linux各**子系统间**事件感知, 采用的是发布/订阅模型, 内核和用户程序间不通过通知链(使用netlink等).
- 通知链允许子系统间共享发生的事件, 无需知道哪些子系统产生事件以及哪些子系统对事件感兴趣.

## (2)角色:
- 接收者(notified): 要求接收某事件的子系统, 会提供回调函数用于调用.
- 通知者(notifier): 感应对应事件并调用callback函数的子系统.

## (3)通知链的类型:
- Atomic notifier chains: callback在中断/原子上下文中执行, 不允许block.
- Block notifier chains: callback在进程上下文中执行, 可以block.
- Raw notifier chains: 对callback, 注册和取消注册都没有限制, 所有的锁和保护由caller提供.
- SRCU notifier chains: Block notifier chains的变种, 同样的限制.

## (4)struct notifier_block:
- notifier_call: 要执行的函数.
- next: 链的下一个元素.
- priority: 优先级, 高优先级的会被先执行, 但一般不使用, 默认都为0.
- 备注:通知链的元素类型.

## (5)备注:
- 代码: include/linux/notifier.h和kernel/notifier.c.

# 二 链定义:
## (1)类型:
- atomic_notifier_head
- blocking_notifier_head
- raw_notifier_head
- srcu_notifier_head

## (2)链注册:
- atomic_notifier_chain_register
- blocking_notifier_chain_register
- raw_notifier_chain_register
- srcu_notifier_chain_register

## (3)链unregister:
- atomic_notifier_chain_unregister
- blocking_notifier_chain_unregister
- raw_notifier_chain_unregister
- srcu_notifier_chain_unregister

## (4)链执行:
- atomic_notifier_call_chain
- blocking_notifier_call_chain
- raw_notifier_call_chain
- srcu_notifier_call_chain

## (5)callback函数返回结果:
- NOTIFY_DONE: 对通知事情不感兴趣.
- NOTIFY_OK: 被正确处理.
- NOTIFY_STOP_MASK: 不再进一步调用.
- NOTIFY_BAD: 调用出错.
- NOTIFY_STOP: NOTIFY_OK|NOTIFY_STOP_MASK.

# 三 常用链:
## (1)netdev_chain:
- 功能: 发送网络设备注册状态的通知信息.
- net/core/dev.c

## (2)inetaddr_chain:
- 功能: 发送本地接口IPv4地址的插入,删除和变更通知信息.

## (3)reboot_notifier_chain:
- 功能: 系统重启时发送通知事件.
