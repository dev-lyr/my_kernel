# 一 概述:
## (1)proc：
- 一个伪文件系统，提供访问和修改内核数据结构的接口.
- 通常挂载在/proc，大部分文件只读，部分可以修改, 从而在系统运行时改变系统配置. 
- 修改方法: sudo bash -c "echo xxx > /proc/yyy", 普通sudo echo xxx > /proc/yyy会提示权限不够, 因为>也需要root权限.
- 数据没有存在块设备上，存放**内存**里，提供内核空间和用户控件的交流通道.

## (2)备注:
- man proc
- Documentation/filesystems/proc.txt
- fs/proc源码

# 二 综合:
## (1)常用系统信息:
- /proc/version: 当前运行的内核版本.
- /proc/cpuinfo
- /proc/meminfo: 被free用来展示系统中空闲和使用内存总量(包括:物理内存和交换内存).
- /proc/vmstat: 显示虚拟内存的统计信息.
- /proc/devices
- /proc/net
- /proc/filesystems: 列出kernel支持的文件系统列表, 若以"nodev"标记则说明该文件系统不需要一个块设备挂载.
- /proc/mounts：当前挂载到系统的文件系统.
- /proc/modules：被load到系统里面的模块列表.
- /proc/interrupts: 用来记录每cpu每IO设备的中断次数.

## (2)系统控制参数查看和修改(/proc/sys目录):
- /proc/sys/kernel
- /proc/sys/dev
- /proc/sys/vm
- /proc/sys/net
- /proc/sys/fs
- 备注:参考sysctl命令.

# 三 进程相关(/proc/pid目录):
## (1)常用:
- /proc/pid/fd和/proc/pid/fdinfo：是个目录，里面每项包含进程打开的文件，文件名为文件描述符，是一个实际文件的符号链接.
- /proc/pid/cmdline：进程执行的完整命令行.
- /proc/pid/environ：进程的环境变量.
- /proc/pid/stat：进程的状态信息，被ps使用.
- /proc/pid/status: 进程的状态信息, 可读性好的.
- /proc/pid/stack: 提供进程的内核栈的函数调用trace, 只有在内核build时设置了CONFIG_STACKTRACE选项才有效.
- /proc/pid/task：包含进程中每个线程的相关信息, 每个线程一个目录.
- /proc/pid/cwd: 到当前进程的工作目录的一个符号链接.
- /proc/pid/exe: 到当前进程的指向的命令的一个符号链接.
- /proc/pid/root: 到进程根目录的一个符号链接, 可通过chroot修改.

## (2)oom-killer相关:
- /proc/pid/oom_adj: 为了兼容兼容先前的kernel而使用该文件来调整badness score, 可选值范围是OOM_ADJUST_MIN(-16)和OOM_ADJUST_MAX(15), 特殊值OOM_DISABLE(-17)关闭该task的oom-killer.
- /proc/pid/oom_score_adj: 在决定那个进程被杀死的情况下添加到对应的badness score. 可选值:OOM_SCORE_ADJ_MIN(-1000)和OOM_SCORE_ADJ_MAX(1000), 最低值-1000相当于关闭oom killer.
- /proc/pid/oom_score: 显示当前的oom-killer score，和oom_score_adj搭配来调整那个进程在out of memory情况下被杀死.

# 四 网络相关(/proc/net):
## (1)常用:
- /proc/net/dev: 系统中网络设备的接收和转发信息统计.
- /proc/net/arp: 内核的arp表.
- /proc/net/route: 内核的路由表.
- /proc/net/sockstat: 套接字统计信息.
- /proc/net/tcp: tcp socket的相关信息.
- /proc/net/udp: udp socket的相关信息.
- /proc/net/unix：unix domain socket相关信息.

# 五 内存相关:
## (1)/proc/meminfo

## (2)/proc/vmstat

## (3)/proc/zoneinfo
