# 一 概述：
## (1)功能:
- 提供系统中运行任务的动态视图.
- 展示系统的汇总信息和被kernel管理的任务的信息.
- 提供交互的接口控制进程操作和私人配置.

## (2)语法:
- top -hv | -bcHisS -d delay -n iterations -p pid [, pid...]

## (3)常用选项:
- -d: 指定刷新间隔, 秒为单位.
- -H: 显示所有线程.

## (4)相关uptime:
- 使用/proc/loadavg文件, 详细man uptime, 超过3性能就有问题.
- 负载包括: 在过去1,5,15分钟内,运行队列中的任务(状态为R:正在运行和等待运行)平均值和等待磁盘IO的任务(状态为D)的平均值.
- 注意: 负载和cpu利用率并不是完全对应.

## (5)备注:
- https://www.linux.com/learn/uncover-meaning-tops-statistics
- 相关: iotop, htop等.

# 二 汇总区:
## (1)概述:
- 读取/proc/stat文件下的信息.

## (2)第一行:
- 当前时间,启动时间,活跃用户和平均负载.
- 相关uptime.

## (3)第二行(Tasks):
- 统计执行的任务的总量, 以及各种运行状态的统计.
- sleeping: 等待某个事件完成(I/O完成或timeout), 包含可中断sleep和不可中断sleep.

## (4)第三行(Cpu(s)):
- us: cpu花费在用户模式的时间比例.
- sy: cpu花费在内核模式的时间比例. 也包含内核线程正在忙着干事情(比如:pdflush和migration线程).
- ni: time running niced user processes.
- id: time spent in the kernel idle handle.
- wa: time waiting for I/O completion.
- hi: 处理硬件中断的时间比例.
- si: 处理软件中断的时间比例.
- st: time stolen from this vm by the hypervisor.
- 备注: 当sy在大多数时间都高于us时, 则表示你的机器可能是作为文件服务器或数据库服务器或类似; 反之, 你的机器可能是在进行大量的数值计算(number crunching).
- 备注: 高hi通常表示设备比较忙, 负载比较高, 特殊情况下设备坏了; 高si并不和真正的中断关联, 软中断是驱动提供的, 因此通常表示需要优化驱动程序.

# 三 任务列属性:
## (1)cpu相关:
- %CPU: 距离上次屏幕刷新任务消耗的cpu时间, 默认是总的cpu时间, 是要**交互命令I**, Irix模式off, 则是总cpu时间/总cpu数量.
- TIME: 自任务启动以来使用的cpu时间.
- TIME+: 类似TIME.
- COMMAND: 用来启动任务的命令行或关联程序.
- S: 进程的状态.

## (2)内存相关:
- %MEM: 当前任务使用的**物理内存**的比例.
- VIRT(kb): 当前任务使用的**虚拟内存**的总量, 包含:代码, 数据, 共享库和被置换出去的页. VIRT=SWAP+RES.
- SWAP(kb): 被swap出去的任务的虚拟内存的总量.
- RES(Resident size, kb): 没有被置换的任务需要的物理内存. RES=CODE+DATA.
- CODE(Code size, kb): 用于可执行代码段的物理内存的大小, 通常也被称为文本段(text resident)或TRS.
- DATA(Data+Stack size, kb): 除了CODE外的物理内存的大小, 通常称为数据段(data resident)或DRS.
- SHR(Shared Mem Size, kb): 任务使用的共享内存的大小.
- nFLT(Page Fault count): 当前任务发送page falut(主要是缺页)的数量.
- nDRT(Dirty Page count): 距离上次写盘到现在, 已被修改的页的数量.

## (3)操作:
- f(交互命令): 选择显示的列, 点击对应字母.
- o(交互命令): 选择排序的行, 小写是向右, 大写向左, 注意列的属性顺序, 不是task的排序.

# 四 交互式命令:
## (1)全局命令:

## (2)汇总区域命令:
- 1: 显示单个cpu的状态.

## (3)任务区域命令:
- f和o: 选择和排序对应属性的显示.
- F和O: 选择任务排序的依据.
- R: 反转排序的顺序.
- H: 显示线程.
- i: 默认显示全部, 点击i显示运行中的任务.
