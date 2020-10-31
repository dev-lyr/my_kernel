# 一 概述:
## (1)概述:
- 功能:包过滤,在linux dynamic tracing, static tracing和profiling events上执行自定义分析程序.
- cbpf(classic bpf): 旧的bpf.
- ebpf(extended bpf) 

## (2)使用:
- 主要推荐的bpf tracing的终端工具是: **bcc**和**bpftrace**.
- 若寻找工具使用, 先尝试bcc然后再是bpftrace.
- 若需要自己编程, 则优先尝试bpftrace再试bcc.
- libbpf库: https://github.com/libbpf/libbpf

## (3)备注:
- http://www.brendangregg.com/ebpf.html
- https://www.kernel.org/doc/html/latest/networking/filter.html
- https://github.com/iovisor/bcc
- https://www.iovisor.org/about
- kernel源码: kernel/bpf
- kernel sample代码: samples/bpf
- bpf系统调用(man 2 bpf)
- https://github.com/cilium/cilium
