# 一 概述:
## (1)读写方式:
- **规范模式**：open文件，O_SYNC和O_DIRECT都为0，内容由read和write来存取，**read阻塞进程**直至数据被拷贝进用户地址空间(允许少于期望的长度)；write在数据被拷贝到page cache后结束.
- **同步模式**：open文件O_SYNC为1或打开后使用fcntl设置为1，只影响write，write操作将阻塞进程，直至数据被有效写入磁盘.
- **内存映射模式**：打开文件后，调用mmap将文件映射到内存，文件称为ram中的一个数组，可以直接访问，无需通过read和write访问.
- **直接IO模式**：O_DIRECT置为1，读写操作都将数据在用户态地址空间和磁盘间直接传送而不通过page cache，通常会降低性能，但是在特定情况下有用，例如程序有自己的缓存(cache).
- **异步IO模式**: libaio和Posix AIO.

## (2)备注:
- 源码: fs/read_write.c

# 二 读取:
## (1)调用路径:
- read->vfs_read->__vfs_read->具体文件系统的read实现.