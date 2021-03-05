# 一 概述:
## (1)概述:
- linux允许挂载同一文件系统多次, 则该文件的root目录通过多个挂载点访问, 但是实际上它是一个, 因为只有一个superblock对象.
- 同一挂载点可以挂载多次(stack), 每个新的mount会隐藏上一个挂载的文件系统, 当最顶层挂载删除时, 下面一层才可见.
- 针对每次挂载, kernel将挂载点和挂载flags等信息保存在内存中一个**vfsmount**对象中.

## (2)struct vfsmount

## (3)备注:
- mount,umount命令和函数

# 二 命名空间:
## (1)概述:
- 创建进程时会继承父进程的namespace, 通过设置CLONE_NEWNS来创建新的namespace.

## (2)struct mnt_namespace:
- count: 使用该ns的进程数量.

## (3)备注:
- fs/mount.h
