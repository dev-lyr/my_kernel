# 一 概述:
## (1)功能:
- 内核检测到严重内部错误并且不能够安全恢复或不能让系统继续执行从而避免更严重问题时所采取的一种安全策略.
- kernel routine通过panic()来处理panic, 通常会在console输出错误信息, dump内核内存到disk, 然后等待系统被手动重启或触发自动重启.
- 引起panic的原因可能是硬件错误或软件bug.
- kdump: linux kernel的特性, 可以在kernel crash时产生crash dumps. kdump导致内存镜像可以在事后debug和分析crash的原因.
- oops: 内核出现不正确行为, 多种类型的oops可导致kernel panic, 但其他一些oops并不会导致系统panic(系统kill受破坏进程继续执行).

## (2)相关内核配置(sysctl -a):
- kernel.panic: 表示当系统遇到panic时等待多少秒reboot.
- kernel.panic_on_oops: 0表示继续操作, 1表示立即panic.
- kernel.softlockup_panic: 0表示继续操作, 1表示当出现softlockup时立即panic.
- kernel.unknown_nmi_panic: 影响处理NMI的行为, 当非0时, 未知NMI被trapped并产出panic.
- kernel.panic_on_unrecovered_nmi
- kernel.panic_on_io_nmi: 控制当cpu接收到由io error导致的NMI(不可屏蔽的中断)时的行为, 0:继续操作, 1立即panic.
- kernel.hung_task_panic: 0继续操作, 默认为0; 1表示系统立即panic.
- vm.panic_on_oom: 0表示系统会杀死流氓进程继续执行; 1表示但当oom发生时(进程不受cgroup的cpuset和mempolicy限制)系统会panic; 2表示即使受cgroup限制, 也会panic; 默认为0.
- panic_on_stackoverflow: 控制当检测到内核, IRQ和异常栈(不包括用户stack)溢出时的行为, 0:继续操作, 1立即panic.

## (3)备注:
- kernel/panic.c
- Documentation/oops-tracing.txt

# 二 coredump：
## (1)概述：
- man 5 core.
- ulimit -a/-c.

## (2)core文件产生：
- 部分信号可产生core dump信息，详见man 7 signal.

## (3)core文件分析：
- gdb: gdb 程序 core文件.

## (4)相关服务:
- kdump: https://www.kernel.org/doc/Documentation/kdump/kdump.txt
- /proc/sysrq-trigger

## (5)相关配置:
- kernel.core_pattern(/proc/sys/kernel/core_pattern)：定位core文件的格式和位置.
- kernel.core_pipe_limit(/proc/sys/kernel/core_pipe_limit): 当core_pattern设置时该配置才生效, 默认为0.
- kernel.core_uses_pid(/proc/sys/kernel/core_uses_id): 在core dump文件名带不带PID.

# 三 call trace:
## (1)概述:
- call trace和体系结构相关.
- dump_stack(): 打印call trace和其它一些信息, lib/dump_stack.c定义默认的dump_stack给没有实现该函数的体系结构使用.

## (2)dump_stack的实现(lib/dump_stack.c):
- dump_stack_print_info(KERN_DEFAULT): 打印一些共有的一样的debug信息, 例如: CPU和PID, Hardware name等.
- show_stack: 具体架构实现不一样, X86的定义在arch/x86/kernel/dumpstack.c文件.
