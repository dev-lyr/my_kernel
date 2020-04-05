# 一 概述:
## (1)概述:
- 根文件系统: root file system, 在系统boot阶段直接被kernel挂载, 包含系统初始化脚本和大量必须的系统程序.
- Rootfs is a special instance of ramfs (or tmpfs, if that's enabled), which is always present in 2.6 systems.You can't unmount rootfs for approximately the same reason you can't kill the init process; rather than having special code to check for and handle an empty list, it's smaller and simpler for the kernel to just make sure certain lists can't become empty.
- Most systems just mount another filesystem over rootfs and ignore it.The amount of space an empty instance of ramfs takes up is tiny.
- If CONFIG_TMPFS is enabled, rootfs will use tmpfs instead of ramfs by default.  To force ramfs, add "rootfstype=ramfs" to the kernel command line.
- 内核参数rootfstype: 设置根文件系统的类型.

## (2)实现:
- **init_rootfs**: 注册rootfs文件系统, 在init/do_mounts.c, 调用方: fs/namespace.c的mnt_init.
- **init_mount_tree**: 安装rootfs文件系统, 在fs/namespace.c.

# 二 init_mount_tree:
## (1)功能:
- 安装rootfs文件系统.

## (2)vfs_kernel_mount

## (3)create_mnt_ns:
- 功能: 创建一个私有的namespace并添加一个root文件系统.
