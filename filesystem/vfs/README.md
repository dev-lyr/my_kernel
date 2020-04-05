# 一 概述：
## (1)VFS功能：
- VFS是一个内核软件层，将不同种类文件系统的共同信息放入内核，支持Linux支持的所有文件系统的任何操作.
- VFS将每个读、写或其它函数，替换为本地linux文件系统、NTFS文件系统或文件所在的其它文件系统的实际函数.

## (2)VFS支持文件系统类型：
- 磁盘文件系统：管理本地磁盘分区中的可用存储空间，例如：linux的Ext3，windows的ntfs等.
- 网络文件系统：允许访问其它机器上文件系统包含的文件.
- 特殊文件系统：例如/proc文件系统.

## (3)文件类型：
- 普通文件
- 目录: vfs把目录当文件对待.
- 字符设备文件
- 块设备文件
- 套接字
- 有名管道
- 符号链接

## (4)符号链接和硬链接区别:
- 硬链接: 直接指向inode节点; 要求链接和文件必须位于同一文件系统; 只有超级用户才能创建目录的硬链接.
- 符号链接: 对一个文件的间接指针, 文件内容是符号链接锁指向的文件的名字; 无文件系统限制; 任何用户可创建; 有自己的inode.
- 相关命令: stat.

# 二 对象类型：
## (1)超级块对象(superblock object,struct super_block)：
- 存放已安装文件系统的有关信息，对于基于磁盘的文件系统，这类对象通常存放于磁盘上的文件系统控制块(filesystem control block).
- 超级块对象由super_block结构组成(fs.h).

## (2)索引节点对象(inode object, struct inode)
- 存放具体文件的信息，对基于磁盘的文件系统，这类对象通常对应于存放在磁盘上的文件控制块(file control block).
- 每个索引节点对象都有一个索引节点号，这个节点号唯一标识文件系统中的文件.
- 索引节点对象由inode结构组成(fs.h).

## (3)文件对象(file object, struct file):
- 包含访问模式、位置偏移等信息.
- 存放打开文件与进程之间进行交互的相关信息，仅当进程访问文件期间存在于内核内存中.
- 文件对象是在文件被打开(open())时创建的，close()调用时销毁(f_count为0时)，由file结构组成，文件对象在磁盘上没有对应映像，因此file结构没有‘脏’字段标记文件对象是否被修改.
- 多个进程打开同一文件时有多个文件对象.
- 父子进程时，子进程与父进程共享父进程已打开文件文件的文件对象(注意是已打开), struct file的f_count记录使用该文件对象的进程数量.
- clone()调用的CLONE_FILES可以设置子进程是否和父进程共享描述符表(descriptor table, struct task_struct的files字段指向内容),files字段count记录使用使用该打开文件表的进程的数量.

## (4)目录项对象(dentry object)：
- 存放目录项与对应文件进行链接的有关信息, 为了方便查找.
- VFS把目录看做由若干子目录和文件组成的一个普通文件，但是一旦目录项被读入内存，VFS把它转换成基于dentry结构的一个目录项对象.
- 对于进程查找路径中的每个分量都会创建一个目录项对象, 目录项对象在磁盘上也没有对应映像.

# 三 与进程相关结构:
## (1)概述:
- struct files_struct *files：文件描述符表. clone的CLONE_FILES控制父子进程间是否共享.
- struct fs_struct * fs: 记录进程的root目录和当前目录.

## (2)files_struct:
- struct file ** fd: 指向件对象指针数组的指针, 数组的索引是文件描述符, 值是文件对象的地址.

# 四 超级块对象:
## (1)struct super_block:
- struct super_operations *s_op: 超级块的方法.
- struct file_system_type *s_type: 文件系统类型.
- struct dentry *s_root: 文件系统根目录的目录项对象.
- struct list_head s_inodes: 所有索引节点对象.
- struct list_head s_inodes_wb: writeback inodes.

## (2)struct super_opeations:
- alloc_inode: 为索引节点对象分配空间, 包括具体文件系统的数据所需要的空间.
- destroy_inode: 撤销索引节点对象, 包括具体文件系统的数据.
- dirty_inode: 当索引节点标记为脏(dirty)调用该函数, 例如:Ext3用该函数来更新磁盘上的文件系统日志.
- write_inode: 更新文件系统的索引节点.

# 五 索引对象:
## (1)struct inode:
- atomic_t i_count: 引用计数.
- struct inode_operations *i_op: 索引节点操作表, 描述VFS操作索引节点对象的所有方法, 这些方法由**文件系统**实现.
- struct file_operations * i_fop: 缺省文件操作.
- unsigned int i_nlink: 硬链接数目.
- unsigned long i_state: 索引节点的状态标志.

## (2)struct inode_operations:
- create: VFS通过系统调用create和open调用该函数, 为指定dentry对象创建一个新的所有节点.
- link: 该函数被系统调用link()调用, 用来创建硬链接.
- unlink: 被系统调用unlink调用, 删除目录中目录项指定的文件的硬连接,i_nlink会减去1, 删除文件时, 内核先检查打开文件的进程个数i_count, 为0再去检查i_nlink，若也为0才会删除文件的内容(释放空间).
- symlink: 被系统调用symlink调用, 创建符号链接.

# 六 目录项对象:
## (1)struct dentry:
- atomic_t d_count: 使用计数.
- struct inode *inode: 相关索引节点.
- struct dentry_operations *d_op: 目录项操作表, 被VFS调用.

## (2)目录项状态:
- 被使用: d_count>0且inode!=null.
- 未被使用: d_count=0且inode!=null.
- 负状态: inode=null.

## (3)目录项缓存.

# 七 文件对象:
## (1)struct file:
- atomic_t f_count: 文件对象的使用计数, 记录使用文件对象的进程数.
- struct file_operations * f_op: 文件操作表, 由**具体的文件系统提供**. 当内核将索引节点从磁盘装入内存时, 就会把文件操作放入索引节点对象的i_fop字段, 当进程打开该文件时, vfs就会用索引对象的i_fop初始化新文件对象f_op字段, 使得文件操作的能够使用这些函数, 如需要vfs可以在f_op存放新的值来修改文件操作集合, 例如:socket.
- struct dentry *f_dentry: 相关目录项对象.
- loff_t f_pos: 文件指针的偏移量.

## (2)struct file_operations:
- read: 由系统调用read调用.
- aio_read: 由系统调用aio_read调用.
- open: 创建一个新的文件对象, 并将其与相应的索引节点对象关联起来, 由系统调用open调用.
- release: 当文件对象的最后一个引用被注销时调用(即f_count为0), 例如: 最后一个共享描述符的进程调用close或退出时, 该函数会被调用.
- poll: 检查文件上是否有操作发生.