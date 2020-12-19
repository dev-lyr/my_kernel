# 一 概述:
## (1)功能:
- kprobes可以动态break into任意kernel routine并收集debugging和performance信息(non-disruptively).
- 可以trap大部分kernel代码地址, 指定一个handler routine, 在hit breakpoint时调用.

## (2)类型:
- kprobes: can be inserted on virtually any instruction in the kernel.
- kretprobes: fires when a specified function returns.

## (3)备注:
- Documentation/kprobe.txt
- kernel/kprobes.c
- 被systemtap,ebpf等使用.
