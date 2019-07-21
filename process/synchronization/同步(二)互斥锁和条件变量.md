# 一 概述:
## (1)互斥锁与条件变量的特点:
- 互斥锁用于上锁, 条件变量用于等待.
- 互斥锁和条件变量可以用于线程或进程间的同步,用于进程间同步时,需放置在多个进程的共享内存区中.
- 互斥锁必须由给它上锁的线程解锁, 任何时刻只有一个线程能够锁住一个给定的互斥锁.
- 静态分配的互斥锁或条件变量具备默认属性, 我们可以利用函数来以非默认属性初始化它们.

## (2)备注:
- 编程技巧: 把共享数据和它们的同步变量(互斥锁、条件变量或信号量)收集到一个结构.

# 二 互斥锁:
## (1)功能:
- 相互排斥, 最基本的同步形式, 用于保护临界区(critical region),以保证任何时刻只有一个线程在执行其中的代码.

## (2)demo:
<pre><code>
lock_the_mutex(...)
临界区 //应该努力减少由一个互斥锁锁住的代码量.
unlock_the_mutex(...)
</code></pre>

## (3)互斥锁的初始化:
- 如果互斥锁是静态分配的, 可以把它初始化为常量: PTHREAD_MUTEX_INITIALIZER.
- 如果互斥锁是动态分配的(例如通过malloc), 或者分配在共享内存区中, 那么必须在运行时通过调用pthread_mutex_init函数来初始化.通过动态分配可以指定进程间共享属性, 从而允许在不同进程间共享某个互斥锁或条件变量, 前提是互斥锁或条件变量必须放在这些进程的共享内存区中.

## (4)上锁或解锁:
- int pthread_mutex_lock(pthread_mutex_t - mptr);//已锁住, 则阻塞
- int pthread_mutex_trylock(pthread_mutex_t - mptr);//不阻塞
- int pthread_mutex_unlock(pthread_mutex_t - mptr);
- 返回值: 成功返回0；若出错则为正的Exxx值.

## (5)备注:
- 如果尝试对一个已由另外某个线程锁住的互斥锁上锁, 那么pthread_mutex_lock将阻塞到该互斥锁解锁位置.
- pthread_mutex_trylock: 是对应的非阻塞函数, 如果该互斥锁已锁住, 它就返回一个EBUSY错误.
- 如果多个线程阻塞在等待同一互斥锁解锁, 那么解锁后将唤醒优先级最高的线程.(互斥锁、条件变量和信号量都一样).

# 三 条件变量:
## (1)条件变量特点:
- 类型为pthread_cond_t.
- 每个条件变量总是由一个互斥锁与之关联.
- 静态分配的条件变量可以初始化为PTHREAD_COND_INITIALIZER.
- 动态分配的条件变量和动态分配的互斥锁一样.可以使用相关函数初始化.

## (2)相关函数:
- int pthread_cond_wait(pthread_cond_t - cptr, pthread_mutex_t *mptr)
- int pthread_cond_signal(pthread_cond_t - cptr)
- int pthread_cond_broadcast(pthread_cond_t - cptr)
- int pthread_cond_timedwait(pthread_cond_t - cptr, pthread_mutex_t *mptr, const struct timespec *abstime)
- 返回值: 成功返回0；若出错则为正的Exxx值.
- 注意: pthread_cond_wait原子地执行以下两个动作: 给互斥锁解锁；把调用线程投入睡眠, 直到另外某个线程就本条件变量调用pthread_cond_signal.pthread_cond_wait返回前重新给互斥锁上锁.

# 四 互斥锁和条件变量的属性:
## (1)互斥锁与条件变量的动态初始化和摧毁:
- int pthread_mutex_init(pthread_mutex_t *mptr, const pthread_mutexattr_t *attr)
- int pthread_mutex_destroy(pthread_mutex_t *mptr)
- int pthread_cond_init(pthread_cond_t *cptr, constr pthread_condattr_t *attr)
- int pthread_cond_destroy(pthread_cond_t *cptr)
- 返回值: 成功返回0；若出错则为正的Exxx值.

## (2)互斥锁与条件变量的属性:
- int pthread_mutexattr_init(pthread_mutexattr_t *attr)
- int pthread_mutexattr_destroy(pthread_mutexattr_t *attr))
- int pthread_condattr_init(pthread_condattr_t *attr)
- int pthread_condattr_destroy(pthread_condattr_t *attr)
- 返回值: 成功返回0；若出错则为正的Exxx值.

## (3)启用和禁止特定属性:
- int pthread_mutexattr_getpshared(const pthread_mutexattr_t *attr, int *valptr)
- int pthread_mutexattr_setpshared(pthread_mutexattr_t *attr, int value)
- int pthread_condattr_getpshared(const pthread_condattr_t *attr, int *valptr)
- int pthread_condattr_setpshared(pthread_condattr_t *attr, int  value)
- 返回值: 成功返回0；若出错则为正的Exxx值.