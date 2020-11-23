# 一 概述:
## (1)概述:
- 功能:包过滤,在linux dynamic tracing, static tracing和profiling events上执行自定义分析程序.
- cbpf(classic bpf): 旧的bpf.
- ebpf(extended bpf) 

## (2)使用:
- 主要推荐的bpf tracing的frontend工具是: **bcc**和**bpftrace**.
- bpftrace is ideal for ad hoc instrumentation with powerful custom one-liners and short scripts, whereas bcc is ideal for complex tools and daemons.
- libbpf库: https://github.com/libbpf/libbpf

## (3)备注:
- http://www.brendangregg.com/ebpf.html
- https://www.kernel.org/doc/html/latest/networking/filter.html
- https://github.com/iovisor/bcc
- kernel源码: kernel/bpf
- kernel sample代码: samples/bpf
- bpf系统调用(man 2 bpf)
