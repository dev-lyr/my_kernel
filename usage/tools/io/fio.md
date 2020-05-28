# 一 fio:
## (1)功能:
- 包装一些进程/线程来执行用户指定的I/O操作.
- 通常用来模拟I/O负载, 进行压测.

## (2)语法:
- fio [options] [jobfile]

## (3)常用选项:
- --output=filename: 将output写入指定文件.
- --timeout=timeout: 限制执行timeout秒.
- --daemonize=pidfile: 后台运行fio, 将进程号写入指定pid文件.
- --client=host: 不在本地运行jobs, 将job发送到指定机器并运行.
- --cmdhelp=command: 显示命令的帮助信息.
- --enghelp
- --showcmd

二 jobfile:
## (1)概述:
- Job文件为ini格式, 包含一个或多个job定义.
- 若jobfile使用-指定, 则jobfile从标准输入读取.
- Global Section: 包含job文件中job的默认参数, 一个job只受在它之前的全局部分的影响, 可以存在任数量的全局部分, job可以覆盖全局部分的参数.

## (2)Job文件参数类型:
- str
- time
- int
- bool
- irange
- float_list

# 三 Job文件参数:
## (1)单位:
- kb_base=int: 1000,1024
- unit_base: 0, 1(基于位), 8(基于字节).

## (2)Job描述:
- name=str
- description=str
- loops=int: 设置迭代执行job的次数, 默认为1.
- numjobs=int: 设置创建一个job的指定clone数量, 每个clone都作为一个独立的线程或进程, 用来创建多个线程/进程来执行同样的操作.

## (3)时间相关:
- runtime=time: 告诉fio执行多久后停止执行.
- time_based: 若设置, fio会持续运行runtime指定时间, 即使已经完成了读/写, fio会循环同样的负载直至runtime到达.
- startdelay=irange(int): 延迟指定job的启动时间.
- ramp_time
- clocksource
- gtod_reduce
- gtod_cpu

## (4)目标文件/设备:
- directory.
- filename=str: fio通常基于job名字, 线程数量和文件number来组成文件名字.
- filename_format

## (5)I/O类型:
- direct=bool: 默认为false, 若设置为true, 则使用non-buffered I/O, 通常O_DIRECT.
- buffered=bool: 默认为true, 表示使用buffered I/O.
- atomic=bool: 若为true, 尝试使用原子direct I/O, 只有Linux支持.
- **readwrite=str, rw=str**: I/O模式类型, 有: read(顺序读), write(顺序写), randread(随机读), randwrire(随机写), rw,readwrite(混合顺序读写), randew(混合随机读写), trim, randtrim, trimwrite.

## (6)Block大小:
- blocksize=int: I/O单元的块的大小(字节为单位), 默认是4096.

## (7)buffer和内存:
- zero_buffers: buffer中初始化为0, 默认填充随机数据.

## (8)I/O size:
- size=int: 一个job中每个线程的文件I/O总大小, fio会运行直至达到设置的size字节, 除非由于其他操作限制运行时间到达, 例如: runtime或io_size.
- io_size.

## (9)I/O engine:
- ioengine: 定义Job触发到文件I/O的类型, 可选: sync, libaio, posixaio, mamp, rdma等.
- io引擎有对应的参数.

## (10)I/O depth:
- iodepth=int: Number of I/O units to keep in flight against the file, 默认为1.
- iodepth_batch_submit
- iodepth_batch_complete_min

## (11)I/O速度:
- rate=int
- rate_min
- rate_iops
- rate_iops_min
- rate_process
- thinktime
- thinktime_spin
- thinktime_blocks

## (12)I/O延迟:
- latency_target
- latency_window
- latency_percentile
- max_latency
- rare_cycle

## (13)I/O repaly
- write_iolog
- read_iolog

## (14)线程,进程和job同步
- thread: 默认使用fork创建job, 若指定则使用pthread_create创建线程.

## (15)Verification

## (16)Steady state

## (17)Measurements and reporting

## (18)Error handling