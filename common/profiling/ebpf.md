# 一 概述:
## (1)概述:
- 功能:包过滤,在linux dynamic tracing, static tracing和profiling events上执行自定义分析程序.

## (2)使用:
- 主要推荐的bpf tracing的终端工具是: **bcc**和**bpftrace**.
- 若寻找工具使用, 先尝试bcc然后再是bpftrace.
- 若需要自己变成, 则优先尝试bpftrace再试bcc.

## (3)备注:
- http://www.brendangregg.com/ebpf.html
- https://www.kernel.org/doc/html/latest/networking/filter.html
- https://github.com/iovisor/bcc
