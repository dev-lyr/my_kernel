# 一 综合：
## (1)系统相关:
- service和chkconfig.
- strace
- ulimit
- sysctl
- yum和rpm

## (2)信息查询:
- sar
- **uptime**: 显示当前时间, 系统开机时间, 当前登录用户数, 以及前1,5,15分钟内的平均负载情况. 平均负载:特定时间内运行队列中进程的平均数, 每个CPU核不超过3代表系统负载良好, 例如:双核CPU, uptime最后显示的不超过6.

## (3)性能测试:
- perf
- stress

# 二 进程相关:
## (1)常用命令:
- ps
- top
- pstack
- pidstat
- mpstat

# 三 网络相关：
## (1)综合查询：
- netstat
- hostname
- ifstat
- iftop

## (2)防火墙相关：
- iptables
- ebtables
- arptables

## (3)http相关.

## (4)dns相关
- host

## (5)tcp相关：
- tcpdump
- tcpreplay
- tcpclient和tcpserver
- tcpcat

## (6)ip和arp相关：
- ipcalc
- arp
- arpd
- arping

## (7)bridge相关：
- brctl

## (8)网卡相关
- ifconfig
- ifstat
- iftop
- ifup和ifdown
- ethtool:显示和修改以太网卡属性.

## (9)路由相关：
- route
- traceroute

## (10)连通性测试.
- ping
- nc
- ssh
- telnet
- curl

## (11)性能测试：
- ab
- netperf(client)和netserver(server)
- http_load

## (12)流量分析：
- tcpdump.
- tcpreplay.
- sar
- tc

# 四 内存相关:
## (1)常用:
- memtester
- vmstat
- free

# 五 IO和磁盘和文件系统相关：
## (1)常用命令:
- iostat
- fio
- dd
- df和du
- sync
- diff
- fdisk
- mount和unmount
- smartctl
- swapon,swapoff和mkswap.

## (2)文件系统相关:
- stat
- lsof和fuser
- file
- fsck

# 六 其它：
## (1)文本处理：
- sed和awk
- tar等
- xargs
- grep和find.

## (2)其它：
- screen.