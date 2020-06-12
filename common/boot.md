# 一 概述:
## (1)概述:
- init/目录下存放系统引导和初始化相关代码.
- start_kernel():完成内核的初始化工作.

## (2)include/linux/init.h:
- 功能: 定义一些宏用来标记一些初始化函数和数据.
- subsys_initcall: 子系统初始化函数, 在启动时候被调用.

## (3)备注:
- https://www.centos.org/docs/5/html/Installation_Guide-en-US/ch-boot-init-shutdown.html
