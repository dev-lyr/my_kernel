# 一概述:
## (1)功能:
- Report Central Processing Unit (CPU) statistics and input/output statistics for devices and partitions.
- 用法: iostat [ -c ] [ -d ] [ -N ] [ -k | -m ] [ -t ] [ -V ] [ -x ] [ -z ] [ device [...] | ALL ] [ -p [ device [,...] | ALL ] ] [ interval [ count ] ]

## (2)常用选项：
- -c: 显示cpu的report
- -d：显示device的report
- -x：display extended statistics.

## (3)实例：
- iostat -x 1：间隔1s查询一次。

# 二 CPU统计：
## (1)%user
- Show the percentage of CPU utilization that occurred while executing at the user level (application).

## (2)%nice
- Show the percentage of CPU utilization that occurred while executing at the user level with nice priority.

## (3)%system
- Show the percentage of CPU utilization that occurred while executing at the system level ## (kernel).

## (4)%iowait
- Show the percentage of time that the CPU or CPUs were idle during which the system had an outstanding disk I/O request.

## (5)%steal
- Show the percentage of time spent in involuntary wait by the virtual CPU or CPUs while the hypervisor was servicing another virtual processor.

## (6)%idle
- Show the percentage of time that the CPU or CPUs were idle and the system did not have an outstanding disk I/O request.

# 三 device统计：
- Device：
gives the device (or partition) name as listed in the /dev directory.

- tps：
Indicate the number of transfers per second that were issued to the device. A transfer is an I/O request to the device. Multiple logical requests can
be combined into a single I/O request to the device. A transfer is of indeterminate size.

- Blk_read/s (kB_read/s, MB_read/s)：
Indicate  the amount of data read from the device expressed in a number of blocks (kilobytes, megabytes) per second. Blocks are equivalent to sectors
and therefore have a size of 512 bytes.

- Blk_wrtn/s (kB_wrtn/s, MB_wrtn/s)：
Indicate the amount of data written to the device expressed in a number of blocks (kilobytes, megabytes) per second.

- Blk_read (kB_read, MB_read)：
The total number of blocks (kilobytes, megabytes) read.

- Blk_wrtn (kB_wrtn, MB_wrtn)：
The total number of blocks (kilobytes, megabytes) written.

- rrqm/s：
The number of read requests merged per second that were queued to the device.

- wrqm/s：
The number of write requests merged per second that were queued to the device.

- r/s：
The number (after merges) of read requests completed per second for the device.

- w/s：
The number (after merges) of write requests completed per second for the device.

- rsec/s (rkB/s, rMB/s)：
The number of sectors(扇区) (kilobytes, megabytes) read from the device per second.

- wsec/s (wkB/s, wMB/s):
The number of sectors (kilobytes, megabytes) written to the device per second.

- avgrq-sz:
The average size (in sectors) of the requests that were issued to the device.

- avgqu-sz:
The average queue length of the requests that were issued to the device.

- await:
The average time (in milliseconds) for I/O requests issued to the device to be served. This includes the time spent by the requests in queue and  the
time spent servicing them.

- r_await:
The average time (in milliseconds) for read requests issued to the device to be served. This includes the time spent by the requests in queue and the
time spent servicing them.

- w_await：
The average time (in milliseconds) for write requests issued to the device to be served. This includes the time spent by the requests  in  queue  and the time spent servicing them.

- %util：
Percentage of CPU time during which I/O requests were issued to the device (bandwidth utilization for the device). Device saturation(饱和) occurs when this value is close to 100%.