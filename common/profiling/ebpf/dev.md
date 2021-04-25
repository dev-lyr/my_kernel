# 一 概述:
## (1)概述:
- Linux期望ebpf程序以bytecode的形式被load.
- 虽然可以直接写字节码, 但更常用是利用编译器(llvm)将pseudo-C代码编译为eBPF字节码.
- eBPF程序通过bpf系统调用来load到linux内核中.
- 当eBPF程序被load到内核后, 在attach到请求的hook前需要做2步: **Verification**和**JIT Compilation**.

## (2)maps:
- eBPF programs can leverage the concept of eBPF maps to store and retrieve data in a wide set of data structures. 
- eBPF maps can be accessed from eBPF programs as well as from applications in user space via a system call.

## (3)相关库:
- libbpf库: https://github.com/libbpf/libbpf
- https://github.com/cilium/ebpf

# 二 bpf系统调用:
## (1)概述:
- 功能: perform a command on an extended BPF map or program.
- 语法: int bpf(int cmd, attr(union bpf_attr指针), unsigned int size)
- 不同cmd对应的bpf_attr属性不一样.

## (2)cmd(bpf_cmd枚举):
- BPF_MAP_CREATE
- BPF_MAP_LOOKUP_ELEM
- BPF_MAP_UPDATE_ELEM
- BPF_MAP_DELETE_ELEM
- BPF_MAP_GET_NEXT_KEY
- BPF_PROG_LOAD: Verify  and  load  an  eBPF  program,  returning  a  new file descriptor associated with the program.

## (3)bpf_attr(cmd=BPF_PROG_LOAD):
- bpf_prog_type prog_type: 对应bpf_prog_type枚举.

## (4)bpf_prog_type:
- BPF_PROG_TYPE_SOCKET_FILTER
- BPF_PROG_TYPE_KPROBE
- 等等.
- 备注: determines the subset of kernel helper functions that the program may call.
