# 一 概述:
## (1)概念
- Each interrupt or exception is identified by a number ranging from 0 to 255; Intel calls this 8-bit unsigned number a **vector**. 
- Each **hardware device controller** capable of issuing interrupt requests usually has a single output line designated as the **Interrupt ReQuest (IRQ) line**.
- All existing IRQ lines are connected to the input pins of a hardware circuit called the **Programmable Interrupt Controller(PIC)**.
- A system table called **Interrupt Descriptor Table(IDT)** associates each interrupt or exception vector with the address of the corresponding interrupt or exception handler.

## (2)中断分类:
- **同步中断**(CPU自身产生,也称为**异常**): 由**cpu控制单元**在执行指令时生产, 称为同步是因为控制单元只会在一个指令执行终止后发出它们. 
- **异步中断(硬件产生, 硬中断)**: 由其他硬件设备依照CPU时钟信号随时产生.
- 备注:Intel将同步中断称为异常, 异步中断称为中断.

## (3)异常产生方式:
- 由程序错误产生,内核通过发送信号来处理异常.
- 由内核必须处理的异常条件产生;例如缺页和系统调用.

## (4)相关文件:
- /proc/interrupts: 记录当前系统中中断的发送情况, 依次为irq序号、上发生中断的次数、可编程中断控制器、设备名称.
- /proc/stat的intr行: 第一个数字是总的中断数量, 后面是指定irq序号(从0开始)的发生次数.
- /proc/irq目录.
- irq_vectors.h
- kernel/irq目录.

## (5)备注:
- 当中断信号到达时,CPU必须停止当前正在做事情,切换到一个新的活动,与进程切换相比,中断切换比较轻量级.
- IRQ:Interrupt Request.
- APIC: Advanced PIC.
- 可控制哪些中断由哪些cpu来处理,可提高cpu处理效率,详见Documentation/IRQ-affinity.txt.

# 二 中断分类:
## (1)可屏蔽中断:
- I/O设备发出的所有中断请求(IRQ)都是可屏蔽中断.
- 可屏蔽中断的状态:屏蔽的(masked)和不可屏蔽的(unmasked).
- 一个可屏蔽中断是屏蔽的,控制单元就会忽略它.

## (2)不可屏蔽中断:
- 危机事件产生(硬件故障)才能引起非屏蔽事件.

# 三 异常分类:
## (1)处理器探测异常(processor-detected exception):
- 故障(fault):通常可以纠正,纠正完毕,重新执行指令,例如：缺页异常处理程序.
- 陷阱(trap).
- 异常中止(abort):发送严重错误,异常中止处理程序只能强制终止受影响的程序.

## (2)编程异常:
- 发生在程序员发出请求时, 通过int或int3指令, into(check for overflow)和bound(check on address bound).
- 通常也**软件中断**(software interrupts).
- 通常用途: **执行系统调用**,给调试程序通报特定事件.

# 四 异常向量:
## (1)概述:
- X86处理器大约发布了20种不同异常, 20~31由intel留作未来开发.
- 内核必须为每种异常提供专门的异常处理程序, 它们通常会把一个Unix信号发生给引起异常的进程.

## (2)常见异常(编号:异常:异常处理程序:信号):
- 0: Devide error: devide_error(): SIGFPE
- 6: Invalid opcode: invalid_op(): SIGILL
- 14: Page Fault: page_fault(): SIGSEGV

# 五 中断描述符表(IDT: Interrupt Descriptor Table):
## (1)概述:
- 用来实现中断向量表, 存放**中断/异常**处理程序的入口地址,Linux可以在每个cpu定义256个IDT项(entries).
- 在IDT中插入门, arch/x86/include/asm/desc.h: set_intr_gate, set_system_intr_gate, set_trap_gate,set_system_trap_gate, set_task_gate.

## (2)中断描述表:
- 0-31: system traps and exceptions.
- 32-127: 设备中断.
- 128: legacy int80 syscall interface.
- 129-INVALIDATE_TLB_VECTOR_START-1(除了204):设备中断.
- INVALIDATE_TLB_VECTOR_START...255:特殊中断.
- 64位X86每个CPU一个IDT表,32位是一个共享的IDT表.
- 备注: 相关文件arch/x86/include/asm/irq_vectors.h.

## (3)IDT包含三种类型描述符(Intel的分类, 40~43位的type表示类型):
- 任务门描述符(task gate)
- 中断门描述符(interrupt gate)
- 陷阱门描述符(trap gate)
- 备注: linux使用中断门来处理中断, 使用陷阱门来处理异常.

## (4)Linux对门的分类:
- 中断门(interrupt gate): 用户态的进程不能访问一个Intel的中断门, 所有的Linux中断处理程序都通过中断门激活, 并全部限制在内核态.
- 系统中断门(system interrupt gate): 能够被用户态进程访问的Intel中断门, 与向量3相关的异常处理程序由系统中断门激活, 用户态可使用汇编指令int3.
- 陷阱门(trap gate): 用户态进程不能访问的一个Intel陷阱门, 大部分linux异常处理程序都通过陷阱门来激活.
- 系统陷阱门(system gate): 用户态的进程可以访问的一个Intel陷阱门, 通过系统门来激活三个Linux异常处理程序, 对应向量是4,5和128, 因此可以在用户态下可以发布into, bound以及int $0x80三条汇编指令, 其中128用来实现系统调用.
- 任务门(task gate): 不能被用户进程访问的Intel任务门, linux对"Double fault"异常的处理程序是由任务门激活的.
