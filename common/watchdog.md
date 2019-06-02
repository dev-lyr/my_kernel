# 一 watchdog/n:
## (1)定义:
- 功能: 检测系统中的soft和hard lockup, 每个cpu core一个watchdog线程.
- soft lockup: 定义一种导致kernel在内核模式循环(loop)超过20s的bug, 不给其它任务执行机会.
- hard lockup: 定义一种导致cpu在内核模式循环(loop)超过10s的bug, 不让其它中断有机会执行.

## (2)相关配置:
- kernel.watchdog: 0表示关闭所有lockup检测; 1表示开启所有lockup检测.
- kernel.watchdog_thresh: 控制hrtimer和NMI事件, soft和hard lockup的阈值,默认为10s, soft lockup阈值是2*watchdog_thresh.
- kernel.soft_watchdog: 0表示关闭soft lockup检测; 1表示开启soft lockup检测.
- kernel.nmi_watchdog: 0表示关闭NMI watchdog(例如:hard lockup); 1表示开启.
- 备注: hard lockup检测每个CPU对timer中断的相应能力, 该机制利用cpu性能计数器寄存器来定期产生NMI(不可屏蔽中断), 一次hard lockup的检测也命名为NMI watchdog.

## (3)备注:
- Documentation/lockup-watchdogs.txt
- kernel/watchdog.c

