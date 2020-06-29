# 一 概述:
## (1)概述:
- 读-拷贝修改: 是一种以空间换时间的同步机制, 用于读性能比较重要的场景, 读者们几乎不需要同步开销, 写者间的同步开销取决于它们的同步机制.
- 可作为读写锁的一种替代, 但当写者比较多时候性能不好.
- include/rcupdate.h
- 文档: Documentation/RCU.

## (2)原理:
- 读者: 标记某块区域是RCU保护的临界区(rcu_read_lock和rcu_read_unlock之间的区域), 在退出临界区前该区域不会被回收, 完成读后通知回收器完成, 以便回收器在grace period时执行写者的update.
- 写者: 写者修改数据前首先拷贝一个被修改元素的副本, 然后在副本上修改, 待修改完成后向回收器(reclaimer)注册一个回调函数(call_rcu)以便在适当时机(grace period)执行真正的修改.

## (3)读者接口:
- rcu_read_lock: 标记某块区域为RCU read-side的临界区开始.
- rcu_read_unlock: 标记某块区域为RCU read-side的临界区结束.
- rcu_dereference

## (4)写者接口:
- synchronize_rcu: 阻塞直至所有**已存在**的RCU read-side临界区读者完成; 或者不block,向reclaimer注册一个callback函数, 当RCU read-side临界区完成后执行, 该callback通常称为call_rcu.
- rcu_assign_pointer
