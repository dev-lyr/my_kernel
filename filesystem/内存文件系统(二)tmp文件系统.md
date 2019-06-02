# 一 概述:
## (1)概述
- tmpfs是一个在**虚拟内存**中存储所有文件的文件系统.
- 当unmount一个tmpfs时, 所有存放在里面的文件会丢失.
- tmpfs puts everything into the kernel internal caches and grows and shrinks to accommodate the files it contains and is able to swap unneeded pages out to **swap space**.

## (2)和ramfs的区别:
- tmpfs是ramfs的派生物, tmpfs可以写数据到swap空间且有一些限制检查(大小), 普通的用户允许写tmpfs.
- ramfs只有root和trusted用户可以写.

## (3)使用场景:
- There is always a kernel internal mount which you will not see at all. This is used for shared anonymous mappings and SYSV shared memory.
- glibc 2.2 and above expects tmpfs to be mounted at /dev/shm for POSIX shared memory (shm_open, shm_unlink).
- Some people (including me) find it very convenient to mount it. e.g. on /tmp and /var/tmp and have a big swap partition. And now loop mounts of tmpfs files do work, so mkinitrd shipped by most distributions should succeed with a tmpfs /tmp.

## (4)备注:
- Documentation/filesystems/tmpfs.txt