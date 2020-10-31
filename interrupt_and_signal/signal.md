# 一 概述：
## (1)定义：
- 信号是软件中断，提供了一种处理异步事件的方法.
- 当引发信号的事件发生时，为进程产生一个信号(或向进程发生一个信号).
- 事件可以是硬件异常(除以0)、软件条件(如：alarm计时器超时)、终端产生的信号或kill函数产生的.
- 每个信号都有一个名字，这些名字都以SIG开头; 在头文件<signal.h>中，这些文件被定义为正整数（信号编号），不存在编号为0的信号.
- **man 7 signal和kill -l 可查询可用信号.**
- **不可靠信号**：信号会丢失；不排队，多次发送同一个信号只收到一次；每次对信号进行处理后，信号动作复位为默认值，需再次调用signal.
- **可靠信号**：信号不会丢失；会对信号排队；调用sigaction对给定信号设置了一个动作，那么在调用sigaction显式改变之前，该设置一直有效.

## (2)常用信号:
- SIGINT(Action:Term): interrupt from keyboard, CTRL+c.
- SIGKILL(Action:Term): kill signal.
- SIGTERM(Action:Term): Terminal signal, 与SIGKILL不同, 该信号可以被捕获, 通常用于要求程序的正常退出.
- SIGOUT(Action:Core): quit from keyboard, CTRL+\\.
- SIGSTOP(Action:Stop): stop进程, 通常是程序发送, 例如: kill.
- SIGTSTP(Action:Stop): Stop typed at terminal, 例如: Ctrl+z.
- SIGCONT(Action: Cont): 若stoped继续执行.
- SIGCHLD(Action:Ign): 子进程stop或终止.

## (3)信号的处理：
- 忽略此信号。大多数信号都可使用这种方式进行处理，但是两种信号缺不能被忽略(SIGKILL和SIGSTOP)。
- 捕捉信号。要通知内核在信号发生时调用一个用户函数，在用户函数中，可执行用户希望对这种事情进行处理。(SIGKILL和SIGSTOP例外，不能被捕捉)
- 执行系统默认动作，大多数信号的系统默认动作是终止进程。
- 备注: SIGKILL和SIGSTOP不能被忽略, 捕捉和阻塞.

## (4)可用的默认动作(man 7 signal):
- Term：终止进程.
- Ign：忽略信号.
- Core：终止进程并dump core,只有部分信号会产生core dump.
- Stop：停止进程, 进程处于T状态.
- Cont：若进程停止则继续进行.

## (5)相关命令和函数：
- kill -l：显示系统支持的信号.
- kill -signal pid：向进程/进程组发送信号, pid可为5类形式: n(n>0);0;-1;-n(进程组为n的所有进程发生信号);commandname.
- pkill -signal name：signal processes based on name and other attributes.
- kill函数：将信号发射给进程或进程组.
- raise函数：允许进程向自己发送信号.
- trap: 当收到指定信号时执行指定的操作.

## (6)signal函数:
- sighandler_t signal(int signum，sighandler_t handler)；
- signum是信号名。
- handler的值是常量SIG_IGN、常量SIG_DEL或当接到此信号后要调用的函数地址。
- SIG_IGN：表示内核忽略此信号。(SIGKILL和SIGSTOP不能忽略和捕捉)
- SIG_DEL：表示接到此信号后的动作是系统默认的动作。
- 当指定函数指针时：则信号发生时，调用该函数。此函数称为信号处理程序或信号捕捉函数.
- 部分系统singal提供不可靠信号，部分提供可靠信号语义，所以最好用sigaction函数代替sigal.

## (7)sigaction函数：
- 提供可靠信号，建议使用它代替signal函数。

# 二 信号集：
## (1)概述：
- 信号集：表示多个信号的集合，数据类型：sigset_t.

## (2)信号集操作函数：
- sigemptyset
- sigaddset
- sigdelset
- sigprocmask
- sigsuspend

# 三 信号与进程：
## (1)概述：
- 每个进程都有一个信号屏蔽字(signal mask)：它规定了当前要阻塞递送到该进程的信号集。
- 信号未决(pending)：在信号产生和信号传递之间的时间间隔内称信号是未决的。
- 如果为进程产生一个选择为阻塞的信号，而且对该信号的动作是系统默认动作或捕捉信号，则为该进程将此信号保持为未决状态，直到：该进程对此信号解除了阻塞；或对此信号的动作更改为忽略。
- fork子进程时，子进程继承父进程的信号处理方式 ，也可设置自己单独的信号处理方式.

## (2)相关函数：
- sigprocmask：检测或更改其信号屏蔽字。仅为单线程的进程定义的，不适合多线程进程。
- sigsuspend(mask)：临时用mask替换当前进程的signal mask，在捕捉到一个信号或发送一个进程终止信号之前，该进程会被挂起；若捕捉到一个信号且从该信号的处理函数返回，则sigsuspend返回，并恢复该进程原有的signal set。

# 四 线程与信号：
## (1)概述:
- 每个线程有自己的信号屏蔽字，但是信号的处理是进程中所有线程共享的.
- 如果信号与硬件或计时器超时有关，则该信号被发送到引起该事件的线程中去，而其他的信号则被发送到任意一个线程。

## (2)相关函数:
- pthread_sigmask：与sigprocmask功能基本相同，除了pthread_sigmask工作在线程中，并且失败时返回错误码而不是设置errno并返回-1.
- sigwait：线程调用sigwait可以等待一个或多个信号的发生。
- pthread_kill：把信号发送给线程。如果信号的默认动作是终止该进程，那么把信号传递给线程会杀掉整个进程。

## (3)经验:
- 使用sigwait可以简化信号处理，允许把异步产生的信号用同步的方式处理。为了防止信号中断线程，可以把信号添加到每个线程的信号屏蔽字中，然后安排专有线程作信号处理.
