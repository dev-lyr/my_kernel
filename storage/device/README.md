# 一 概述:
## (1)基本设备类型(linux驱动程序):
- 字符设备
- 块设备
- 网络接口

## (2)相关文件:
- fs/block_dev.c: 块设备
- fs/char_dev.c: 字符设备
- include/linux/fs.h
- include/linux/cdev.h
- include/linux/kobject.h

## (3)相关命令:
- mknod
- mkfs
- fdisk
