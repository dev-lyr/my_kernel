# 一 概述:
## (1)概述:
- eBPF可以在不修改内核代码和不加载kernel modules的情况下载内核中运行sandboxed程序.
- cbpf(classic bpf): 旧的bpf, tcpdump使用, 如今linux内核只会运行ebpf, loaded cbpf会被透明的翻译为ebpf.

## (2)术语:
- bpf虚拟机
- bpf验证器
- JIT编译器
- bpf映射
- bpf指令
- 执行点
- bpf程序类型
- 帮助函数

## (3)使用:
- 主要推荐的bpf tracing的frontend工具是: **bcc**和**bpftrace**.
- bpftrace: is ideal for ad hoc instrumentation with powerful custom one-liners and short scripts.
- bcc: is ideal for complex tools and daemons.
- 若寻找工具使用则优先尝试bcc, 若需要编写自己的工具则优先尝试bpftrace.
- libbpf库: https://github.com/libbpf/libbpf

## (4)备注:
- https://ebpf.io/
- http://www.brendangregg.com/ebpf.html
- https://www.kernel.org/doc/html/latest/networking/filter.html
- https://github.com/iovisor/bcc
- kernel源码: kernel/bpf
- kernel sample代码: samples/bpf
- man bpf-helpers
- bpf系统调用(man 2 bpf)

# 二 功能:
## (1)Networking
- The combination of **programmability and efficiency** makes eBPF a natural fit for all packet processing requirements of networking solutions.
- The **programmability** of eBPF enables adding additional protocol parsers and easily program any forwarding logic to meet changing requirements without ever leaving the packet processing context of the Linux kernel. 
- The **efficiency** provided by the JIT compiler provides execution performance close to that of natively compiled in-kernel code.

## (2)Tracing&Profiling:
- The ability to attach eBPF programs to **trace points** as well as kernel and user application **probe points** allows unprecedented visibility into the runtime behavior of **applications and the system** itself.

## (3)Observability&Monitoring:
- Instead of relying on static counters and gauges exposed by the operating system, eBPF enables the collection & **in-kernel aggregation** of custom metrics and generation of visibility events based on a wide range of possible sources.

## (4)Security:
- Building on the foundation of seeing and understanding all system calls and combining that with a packet and socket-level view of all networking operations allows for revolutionary new approaches to securing systems.

