# 一 概述:
## (1)相关文件:
- Document/sysctl/vm.txt: 所有内存相关配置选项的介绍.

# 二 脏(dirty)页相关:
## (1)dirty_background_ratio和dirty_background_bytes:
- dirty_background_bytes: Contains the amount of dirty memory at which the background kernel
**flusher** threads will start writeback.
- dirty_background_ratio: Contains, as a percentage of total available memory that contains free pages
and reclaimable pages, the number of pages at which the background kernel
**flusher** threads will start writing out dirty data.
- 备注: 两者类似, 同时只需指定一个.

## (2)dirty_ratio和dirty_bytes:
- dirty_bytes: Contains the amount of dirty memory at which a process generating disk writes
will itself start writeback.
- dirty_ratio: Contains, as a percentage of total available memory that contains free pages
and reclaimable pages, the number of pages at which a process which is
generating disk writes will itself start writing out dirty data.

## (3)dirty_writeback_centisecs:
- The kernel flusher threads will periodically wake up and write `old' data
out to disk.  
- This tunable expresses the interval between those wakeups, in
100'ths of a second.

## (4)dirty_expire_centisecs:
- This tunable is used to define when dirty data is old enough to be eligible
for writeout by the kernel flusher threads.  
- It is expressed in 100'ths of a second.  
- Data which has been dirty in-memory for longer than this interval will be written out next time a flusher thread wakes up.

# 三 交换(swap)相关:
## (1)swappiness:
- 功能: 设置使用swap空间的积极性, 可选是0-100, 默认是60, 值越高越积极.

# 四 缓存(cache)相关:
## (1)drop_caches:
- 1: 回收页缓存(pagecache).
- 2: 回收slab对象(dentries和inode).
- 3: 回收pagecache和slab对象.
- 备注: 非破坏性操作, 不会free任何dirty对象, 为了free更多对象, 可以先执行下sync.
- 备注: 使用该配置会导致性能问题, 因为drop被缓存的对象, 会导致大量的io和cpu用来drop对象，特别在负载比较高的情况下.

## (2)vfs_cache_pressure:
- 控制内核回收目录和inode对象的cache的内存的倾向, 默认值为100, 表示kernel公平的回收dentry和inode对象, 与pagecache和swapcache一样.
- 当为0时, kernel不会回收dentry和inode cache, 容易导致oom.
- 大于100，kernel优先回收dentry和inode cache, 会导致性能影响.

# 五 oom相关:
## (1)panic_on_oom:
- 0: 默认, kernel调用oom-killer杀死流氓进程, 系统存活.
- 1: 当oom时系统会panic, 例外:进程被cgroup的mempolicy/cpusets限制, 此时杀死进程, 不panic.
- 2: 系统立即panic, 配合kdump可观察oom发生原因.

## (2)oom_kill_allocating_task:
- 0: 默认, oom-killer查看全部任务列表基于启发式算法选择一个任务杀死, 通常选择一个占用大量内存的流氓进程.
- 非0: oom-killer杀死引起触发oom的任务, 避免了昂贵的全部任务列表扫描.

## (3)/proc/pid/目录(单个进程级别):
- oom_adj: 为了兼容兼容先前的kernel而使用该文件来调整badness score, 可选值范围是OOM_ADJUST_MIN(-16)和OOM_ADJUST_MAX(15), 特殊值OOM_DISABLE(-17)关闭该task的oom-killer.
- oom_score_adj: 在决定那个进程被杀死的情况下添加到对应的badness score. 可选值:OOM_SCORE_ADJ_MIN(-1000)和OOM_SCORE_ADJ_MAX(1000), 最低值-1000相当于关闭oom killer.
- oom_score: 显示当前的oom-killer score，和oom_score_adj搭配来调整那个进程在out of memory情况下被杀死.

# 六 内存分配相关:
## (1)overcommit_memory:
- 0: 默认, 当用户空间请求更多内存时, kernel尝试评估空闲内存(某种算法), 若有则满足; 反之则返回失败.
- 1: 来者不拒, kernel假装内存充足, 直至oom.
- 2: 不允许超额分配(never overcommit).
- 备注: 这里只是内存申请, 并不是内存的实际分配.

## (2)overcommit_ratio和overcommit_kbytes:
- 当overcommit_memory设置为2时, commited地址空间不允许超过(交换空间+物理内存*overcommit_ratio).