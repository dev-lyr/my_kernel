# 一 概述:
## (1)概述:
- JBD(Journaling Block Device): 提供与文件系统独立的文件系统日志接口,有2个版本(jbd和jdb2),ext3和ext4都使用jdb2.
- 非日志型文件系统的缺点: 文件更新会在内存保留一段时间才会才会刷新到磁盘, 若遇到系统崩溃或掉电等不可预测事件, 则会导致文件系统处于不一致状态, 因此文件系统需要在安装之前进行一个彻底的, 耗时的检查, 并修正磁盘上文件系统的所有数据结构. 检查时间取决于文件检查的数量, 也取决于磁盘大小(几百G可能需要几个小时), 因此造成的停机时间对于任何生产环境和高可用服务器都是无法接受.

## (2)原理:
- 将文件系统的修改操作分为3步: 1.将待写块的副本放入日志; 2.待1完成后才将更新数据写入文件系统;3.待2完成后删除日志中的副本.
- 先写日志后操作.
- 事务T开始执行前, 先记录T start到日志; 在每个T的写操作之前先写日志; 当T提交时, 记录T commit到日志文件中; 当I/O真正完成后, 会从日志文件中把事务删除掉. **在日志记录写出到稳定存储之前不能真正的更新数据**.
- 若日志包含T start没有T commit则事务T需撤销; 若包含T commit则事务需重做.

## (3)Ext4和JDB之间交互的基本单元:
- 日志记录: 描述日志文件系统一个磁盘块的一次更新.
- 原子操作处理: 包含文件系统一次高级修改对应的日志记录; 一般修改文件系统的每个系统调用都引起一个原子操作处理.
- 事务: 包含几个原子操作处理. 

## (4)日志系统的三种模式:
- ordered: 默认.
- journal
- writeback
- 参考: mount命令的data参数.

## (5)相关文件:
- fs/jbd2: 通用的jdb代码.
- fs/ext4/ext4_jbd2.c: ext4特定扩展.
- Documentation/filesystems/ext4.txt
- /proc/fs/jbd2

## (6)备注:
- 日志型文件系统: Ext3, Ext4.
- 非日志型文件系统: Ext2.
- 相关机制: **WAL**.
- 相关命令:fsck.

# 二 事务:
## (1)概述:
- 为了效率, JDB将多个原子操作处理的日志记录分组放在一个事务里, 与一个原子处理相关的日志记录都必须包含在同一事务.
- 一个事务的所有日志记录存放在日志的连续块中, JDB层把每个事务作为整体处理. 
- 当一个事务的日志记录中的所有数据都提交到文件系统后才会回收该事务使用的块.
- 事务创建后就可以接收新的事务, 停止接收的条件: (1)固定时间过去, 通常为5s; (2)日志中没有空闲块留给新处理.
- 事务数据结构为transaction_t.
- 任何时刻, 日志中可能包含多个事务, 但只有一个处理T_RUNNING状态.
- **只有JDB确认日志记录描述的所有缓冲区都已写入文件系统后, 才会在日志文件中删除事务**.

## (2)状态(t_state):
- 完成: 对应状态T_FINISHED,事务中所有日志记录都物理上写入日志, 当故障恢复时e2fsck会将每个完成的事务相关的块写入文件系统, 即redo.
- 未完成: 事务中至少还有一个日志记录没有物理写入日志, 或者还在接收新的日志记录, 系统故障时, uncommitted事务会被撤销, 对应状态T_RUNNING(还在接收新的原子处理操作), T_LOCKED(不接收新的原子处理操作, 但其中一些还未完成), T_FLUSH(原子操作都已完成, 但一些日志记录还在写入日志), T_COMMIT(原子操作所有日志记录都已写入日志).

# 三 jdb2内核线程:
## (1)创建:
- journal.c的jbd2_journal_start_thread函数负责创建和启动jdb2线程, 该函数在mount文件系统时被调用, 例如ext4的mount操作中, 执行函数为kjournald2: 用来管理日志设备(logging device).

## (2)kjournald2函数:
- COMMIT: commit文件系统当前的状态到disk, journal线程负责将metadata buffers写入disk;
- CHECKPOINT: flushing日志中旧的buffers来回收空间.

# 四 journal_t结构:
## (1)概述:
- 包含单个文件系统的所有journaling state信息.
- include/linux/jdb2.h中定义.

## (2)事务相关字段:
- j_running_transction: 当前正在运行的事务.
- j_committing_transction: 正在pushing到磁盘.
- j_checkpoint_transctions: 一个存放所有等待checkpointing的事务的一个循环list.
- j_wait_transaction_locked.
- j_wait_done_commit
- j_wait_commit
- j_wait_updates
- j_commit_callback: 事务被close后的callback.

## (3)时间相关:
- j_min_batch_time
- j_max_batch_time
