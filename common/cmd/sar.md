# 一 概述:
## (1)功能：
- 收集,报告和存储系统活动信息.

## (2)常用选项:
- -b: report I/O and transfer rate statistics:
- -B: report paging statistics:
- -d: report activity for each block device.
- -f [filename]: 从filename抓取数据, 默认是日常数据文件/var/log/sa/sadd.
- -i interval: 收集数据的间隔, 秒为单位.
- -n{keyword [,...] | ALL}: 报告网络统计信息.
- -o [filename]: 把收集数据保存到filename, 默认是/var/log/sa/sadd.
- -q: report queue length and load averages.
- -r: report memory utilization statistics.
- -R: report memory statistics.

# 二 磁盘相关选项.
## (1)-b:
- 功能: Report I/O and transfer rate statistics.
- tps: 每秒对物理磁盘的I/O请求数, 备注: 多个逻辑请求会被合并为一个单个I/O请求.
- rtps: 读I/O次数.
- wtps: 写I/O次数.
- bread/s: 每秒从设备读取的块(block)数量, 块等于扇区,即512字节.
- bwrtn/s: 每秒写入设备的块数量.

## (2)-d:
- 功能: 显示每个块设备的活动情况.
- tps: 每秒到设备的transfer的数量.
- rd_sec/s: 每秒从设备读取的扇区(sector)的数量, 一个扇区的大小为512字节.
- wr_sec/s: 每秒向设备写的扇区(sector)的数量, 一个扇区的大小为512字节.
- avgrq-sz: The average size (in sectors) of the requests that were issued to the device.
- avgqu-sz: The average queue length of the requests that were issued to the device.
- await: The  average  time (in milliseconds) for I/O requests issued to the device to be served.包括排队时间和服务时间.
- %util: Percentage  of  elapsed  time  during  which  I/O requests were issued to the device (bandwidth utilization for the device). Device saturation occurs  when this value is close to 100%.
 

# 三 网络相关:
## (1)-n:
- 语法: sar -n {keyword [,...] | ALL}, keyword代表显示哪一类别的属性.
- keyword种类: DEV, EDEV, NFS, NFSD, SOCK, IP, ICMP, TCP, UDP等.

## (2)DEV:
- IFACE: 网络接口的名字.
- rxpck/s: 每秒接收(receive)的包的数量.
- txpck/s: 每秒发送(transmit)的包的数量.
- rxkB/s: 每秒接收的千字节(kilobytes)的数量.
- txKB/s: 每秒发送的千字节(kilobytes)的数量.
- rxcmp/s: 每秒接收的compressed包的数量.
- txcmp/s: 每秒发送的compressed包的数量.
- rxmcst/s: 每秒接收到多播(multicast)包的数量.

## (3)EDEV:
- IFACE: 网络接口的名字.
- rxerr/s: 每秒接收的bad包的数量.
- txerr/s: 每秒发送包时出现error包的数量.
- rxdrop/s: 收包时,每秒由于linux buffer空间不足导致drop的数量.
- txdrop/s: 发包时,每秒由于linux buffer空间不足导致drop的数量.
- coll/s: 发送包时, 每秒出现冲突(collision)的数量.
- txcarr/s: Number of carrier-errors that happened per second while transmitting packets.
- rxfram/s: Number  of  frame alignment errors that happened per second on received packets.
- rxfifo/s: Number of FIFO overrun errors that happened per second on received packets.
- txfifo/s: Number of FIFO overrun errors that happened per second on transmitted  packets.

# 四 内存相关:
## (1)相关选项:
- -B: 显示页(page)相关统计.
- -r: 显示内存使用统计.
- -R: Report memory statistics.
- -H: 显示hugepage使用统计.
- -S: 显示swap空间使用统计.
- -W: 显示swapping相关统计.

# 五 CPU相关:
## (1)相关选项:
- -q: Report queue length and load averages.
- -u [ALL]: Report CPU utilization.
- -P {cpu [,...] | ALL}: Report per-processor statistics for the specified processor or processors.
- 相关命令: mpstat.

## (2)-q:
- runq-sz: 运行队列长度(等待时间片的任务数量).
- plist-sz: 任务列表的任务长度.
- ldavg-1: 过去1分钟的负载情况.
- ldavg-5: 过去5分钟的负载情况.
- ldavg-15: 过去15分钟的负载情况.
- blocked: 当前阻塞等待I/O完成的任务的数量.
- 负载计算方式: 可运行或运行中(状态为R)任务的平均数量和不可中断任务(状态为D)的过去时间间隔的数量.

## (3)-q/-P:
- %user: Percentage of CPU utilization that occurred while executing at the user level (application). Note that this field includes time spent running virtual processors.
- %usr: Percentage of CPU utilization that occurred while executing at the user level (application). Note that this field does NOT include time spent running virtual processors.
- %nice: Percentage of CPU utilization that occurred while executing at the user level with nice priority.
- %system: Percentage of CPU utilization that occurred while executing at the system level (kernel). Note that this field includes time spent servicing hardware and software interrupts.
- %sys: Percentage of CPU utilization that occurred while executing at the system level (kernel). Note that this field does NOT include time spent servicing hardware or software  interrupts.
- %iowait: Percentage of time that the CPU or CPUs were idle during which the system had an outstanding disk I/O request.
- %idle: Percentage of time that the CPU or CPUs were idle and the system did not have an outstanding disk I/O request
- %steal: Percentage of time spent in involuntary wait by the virtual CPU or CPUs while the hypervisor was servicing another virtual processor.
- %irq: Percentage of time spent by the CPU or CPUs to service hardware interrupts.
- %soft: Percentage of time spent by the CPU or CPUs to service software interrupts.
- %guest: Percentage of time spent by the CPU or CPUs to run a virtual processor.
- %gnice: Percentage of time spent by the CPU or CPUs to run a niced guest.

