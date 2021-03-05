# 一 概述:
## (1)概述:
- The page cache is the main disk cache used by the Linux kernel. In most cases, the kernel refers to the page cache when **reading** from or writing to disk. New pages are added to the page cache to satisfy User Mode processes's read requests. If the page is not already in the cache, a new entry is added to the cache and filled with the data read from the disk. If there is enough free memory, the page is kept in the cache for an indefinite period of time and can then be reused by other processes without accessing the disk.
- Similarly, before **writing** a page of data to a block device, the kernel verifies whether the corresponding page is already included in the cache; if not, a new entry is added to the cache and filled with the data to be written on disk. The I/O data transfer does not start immediately: the disk update is delayed for a few seconds, thus giving a chance to the processes to further modify the data to be written (in other words, the kernel implements deferred write operations).


## (2)页缓存类型:
- page containing date of regular files
- page containing directories
- page containing data directly read from block device files(skipping filesystem layer)
- Pages containing data of User Mode processes that have been swapped out on disk.
- Pages belonging to files of special filesystems, such as the shm special filesystem used for Interprocess Communication (IPC) shared memory region.

## (3)buffer:
- In old versions of the Linux kernel, there were two different main disk caches: the **page cache**, which stored whole pages of disk data resulting from accesses to the contents of the disk files, and the **buffer cache**, which was used to keep in memory the contents of the blocks accessed by the VFS to manage the disk-based filesystems.
- Starting from stable version 2.4.10, the buffer cache does not really exist anymore. In fact, for reasons of efficiency, block buffers are no longer allocated individually; instead, they are stored in dedicated pages called "buffer pages ," which are kept in the page cache.

## (4)备注:
- 参考深入理解linux内核.
