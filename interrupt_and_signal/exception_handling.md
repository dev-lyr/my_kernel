# 一 概述:
## (1)概述:
- CPU发出的大部分exception会被linux解释为error conditions, 当它们发生时, Kernel会给导致该exception的进程发送一个**signal**, 通知该进程一个anomalous condiiton.
- 例如: 进程执行除0操作时, CPU发出一个**Divide error**异常, 对应的**异常handler**发送一个SIGFPE信号给当前进程, 该进程执行下一步操作(恢复或终止).

## (2)异常处理步骤:
- Save the contents of most registers in the Kernel Mode stack.
- Handle the exception by means of a high-level C function.
- Exit from the handler by means of the ret_from_exception function.
