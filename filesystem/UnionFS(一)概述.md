# 一 概述:
## (1)功能:
- **Unionfs** is a filesystem service for Linux, FreeBSD and NetBSD which implements a **union mount** for other file systems.
- It allows files and directories of separate file systems, known as branches, to be transparently overlaid, forming a single coherent file system.
- Contents of directories which have the same path within the merged branches will be seen together in a single merged directory, within the new, virtual filesystem.
- **union mounting** is a way of combining multiple directories into one that appears to contain their combined contents.

## (2)相关实现:
- aufs
- overlay/overlay2: Documentation/filesystems/overlayfs.txt.
- unionfs-fuse

## (3)备注:
- https://en.wikipedia.org/wiki/UnionFS
- 使用场景: docker镜像等.