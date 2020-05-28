# 一 概述:
## (1)相关网站:
- http://www.brendangregg.com/linuxperf.html

## (2)相关工具:
- stress
- sysbench: https://github.com/akopytov/sysbench, 
- unixbench: https://github.com/kdlucas/byte-unixbench, 是系统benchmark, 不是cpu, mem或disk benchmark.

# 二 网络相关：
## (1)常用工具：
- ab
- httperf
- netperf
- tcpdump

## (2)常用指标：
- BPS(b/s): 例如: 万兆网卡为10Gb/s.
- PPS(p/s)
- QPS
- TPSs
- RTT(Round Trip Time)
- PV(Page View)

## (3)备注:
- http://www.cisco.com/c/en/us/about/security-center/network-performance-metrics.html

# 三 磁盘相关：
## (1)常用工具：
- fio.
- iostat
- iometer
- iotop

## (2)常用指标：
- IOPS：单位时间内系统能处理的I/O请求数，即每秒能处理IO请求数，IO请求分为读请求(随机Random或顺序Sequential)和写请求(随机Random或顺序Sequential).
- 吞吐量(throughout)：单位时间内最大的I/O流量.
- 延迟(latency)：处理单个IO请求的时间.

## (3)经验：
- 在web、数据库和邮件等小文件频繁读写情况下，性能由IOPS决定;
- 在视频等大文件读写情况下，性能由吞吐量决定.
- 应用程序单个IO请求的时间应该是处理时间+等待时间.
- 数据库系统对延迟比较敏感.
- IO queue会增加延迟，但提高IOPS.

## (4)参考:
- http://louwrentius.com/understanding-iops-latency-and-storage-performance.html
https://en.wikipedia.org/wiki/IOPS

# 四 进程相关:
## (1)常用工具：
- stress/stress-n
- top

## (2)常用指标：
- hz

# 五 内存相关:
## (1)常用工具：
- vmstat
- memtest86

# 六 文件系统相关：
## (1)常用工具：
- lsof