# 一 概述:
## (1)概述:
- BPF is a highly flexible and efficient virtual machine-like construct in the Linux kernel allowing to execute bytecode at various **hook points** in a safe manner.

## (2)Hook:
- eBPF程序是事件驱动, 可在程序或内核传递一个确定hook点执行; 预定义(pre-defined)的hooks包含: 系统调用, 函数进入/退出, kernel tracepoints, network events和其它.
- 若预定义的hook不存在, 就需要创建一个kernel probe(kprobe)或user probe(uprobe)来attach eBPF程序到内核或应用程序.

## (3)备注:
- include/uapi/linux/bpf.h
- tools/lib/bpf
- https://docs.cilium.io/en/stable/bpf/
- https://ebpf.io/what-is-ebpf/#introduction-to-ebpf
