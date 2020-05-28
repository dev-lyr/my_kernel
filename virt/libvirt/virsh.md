# 一 概述:
## (1)安装:
- yum install libvirt来安装virsh。
- 参考: http://libvirt.org/virshcmdref.html

## (2)概述:
- virsh是libvirt对应的shell命令.
- The virsh program is the main interface for managing virsh guest domains.
- All virsh operations rely upon the libvirt library.

## (3)用法:
- virsh [OPTION]... COMMAND [ARG]...
- irsh [OPTION]... [COMMAND_STRING]

# 二 常用子命令:
## (1)Domain管理(virsh help domain):
- create: 从xml文件创建一个domain(会启动).
- define: 从xml文件创建一个domain(不启动), 状态为shut off.
- start: 启动一个先前定义的domain, 状态为running。
- shutdown: 温柔的shutdown一个domain, 状态为shutdown.
- destroy: destroy(stop) a domain，状态为shut off，可以start.
- suspend和resume: suspend和resume a domain.
- undefine: undefine a domain.
- dump: dump the core of a domain to a file for analysis
- dumpxml: domain information in XML.
- vcpucount: domain vcpu counts.
- vcpuinfo: domain vcpu详细信息.
- setvcpus: 设置virtual cpu数量.

## (2)Domain监视(virsh help monitor):
- dominfo: domain信息.
- list: list domain.
- domblklist: list all domain blocks.
- domblkinfo
- domiflist: 列出所有domain虚拟接口.
- domifstat: 列出单个接口的信息.

## (3)Host和Hypervisor(virsh help host):
- sysinfo: 展示hypervisor sysinfo.
- nodeinfo: 展示node信息.

## (4)Interface(virsh help interface，操作host interfaces):
- iface-list: 列出物理host interfaces.

## (5)Network Filter(virsh help filter).

## (6)Networking(virsh help network，virtual network).

## (7)Node Device(virsh help nodedev).

## (8)Snapshot(virsh help snapshot).

## (9)Storage pool(virsh help pool: 下面命令操作存储池)

## (10)Storage Volume(virsh help volume)

## (11)Secret(virsh help secret)

## (12)virsh自身(virsh help virsh):
- connect: 连接到hypervisor.

# 三 domain管理

# 四 Domain监控:
## (1)domain的8个状态(STATE):
- running: domain正在一个cpu上running.
- idle: domain在等待io或由于没有事情做进入sleep状态.
- paused: domain被暂停, 通常是管理员调用virsh suspend, pause状态的domain仍然占有分配的资源, 例如内存,但不会被hypervisor调用.
- shutdown: domain在shutdown过程中, guest os已被通知并且应该在平滑停止操作过程.
- shut off: domain没有运行, 通常表示domain已经被完全关闭或还没被启动.
- crashed: domain已经crashed, 通常表示一个violent ending.
- dying
- pmsuspended

## (2)list:
- 功能: list domian.
- 用法: virsh list [--inactive] [--all], 默认--inactive.
