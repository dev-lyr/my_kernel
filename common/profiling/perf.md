# 一 概述:
## (1)概述:
- perf别名: perf_events, performance counters for linux(PCL), Linux perf events(LPE).
- perf是一个**面向事件**的观测工具, 可以帮助解决高级性能和troubleshooting问题.
- 功能: instrument CPU performance counters, tracepoints, kprobes, and uprobes (dynamic tracing).

## (2)语法:
- perf [--version] [--help] [OPTIONS] COMMAND [ARGS]

## (3)常用COMMAND:
- perf list: List all symbolic event types.
- perf top: System profiling tool.
- perf stat: Run a command and gather performance counter statistics.
- perf record: Run a command and record its profile into perf.data.
- perf report: Read perf.data (created by perf record) and display the profile.
- perf probe: Define new dynamic tracepoints.
- perf trace: strace inspired tool.

## (4)模式:
- 计算(perf stat)
- 采样(perf record)

## (5)备注:
- tools/perf
- kernel/events
- https://perf.wiki.kernel.org/index.php/Main_Page
- http://www.brendangregg.com/perf.html

# 二 event:
## (1)概述:
- include/uapi/linux/perf_event.h
- man 2 perf_event_open

## (2)事件类型:
- 硬件事件(PERF_TYPE_HARDWARE)
- 软件事件(PERF_TYPE_SOFTWARE)
- Kernel tracepoint event(PERF_TYPE_TRACEPOINT)
- User Statically-Defined Tracing(USDT)
- 动态追踪(Dynamic Tracing)内核软件使用kprobes,应用软件使用uprobes.
- 等等

# 三 perf top:
## (1)功能:
- 实时生成和显示performance counter profile.

## (2)语法:
- perf top [-e <EVENT> | --event=EVENT] [<options>]

## (3)常用选项:
- -a/--all-cpus: 默认,系统范围的收集.
- -c <count>, --count=<count>: Event period to sample.
- -C <cpu-list>, --count=<count>: 监视指定的cpu.
- -d <seconds>, --delay=<seconds>: 刷新间隔.
- -e <event>,--event=<event>: 选择PMU(Performance Monitor Unit)事件, event可以是symbolic事件名字(perf list列出的所有事件)或raw PMU事件(eventsel+umask).
- **-g**: Enables call-graph (stack chain/backtrace) recording.
- -p <pid>, --pid=<pid>: Profile指定进程的event, 若是列表以逗号分隔.
- -t <tid>, --tid=<tid>: Profile指定线程的event, 若是列表以逗号分隔.
- -K, --hide_kernel_symbols: 隐藏kernel symbols.
- -U, --hide_user_symbols: 隐藏user symbols.
- --fields=: 指定输出列, 可用:overhead, overhead_sys, overhead_us, overhead_children, sample和period.

# 四 perf-stat:
## (1)概述:
- 执行一个命令并收集performance counter statistics.

## (2)语法:
- perf stat [-e <EVENT> | --event=EVENT] [-a] — <command> [<options>]
- perf stat [-e <EVENT> | --event=EVENT] [-a] record [-o file] — <command> [<options>]
- perf stat report [-i file]

## (3)选项:
- -p: stat events on existing process id.
- -e
- report
- record

# 五 perf-record

# 六 perf-report
