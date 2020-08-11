# 一 概述:
## (1)功能:
- linux内核提供一种机制, 可以限制、记录和隔离进程组所使用的物理资源(cpu, mem, io等).

## (2)相关概念:
- **任务(task)**:在cgroups中,任务就是进程.
- **控制组 (control group)**:按照某种标准划分的**进程**，cgroups中**资源控制以控制组为单位进行**，一个进程可以加入和退出一个控制组.
- **层级 (hierarchy)**:控制组可以组织成分层形式(一颗控制组树)，子节点继承父节点的一些属性.
- **子系统 (subsystems)**:一个子系统就是一个**资源管理器**，比如cpu子系统，mem子系统等, 每个子系统对于一个挂载点.

## (3)用法:
- 每个子系统对于一个挂载点, 例如:mount{cpuset = /cgroup/cpuset}
- 每个cgroup是子系统挂载点目录下面的一个子目录, 比如:/cgroup/cpuset/producer, 对于producer这个cgroup.
- 每个cgroup目录下的**tasks**文件表示该cgroup下进程的id.
- 每个cgroup在相关子系统的限制属性通过该cgroup目录下的相关文件进行限制, 例如: /cgroup/cpuset/producer/cpuset.cpus.
- 备注: 上述操作可以通过配置文件也可以手动命令行操作.

## (4)相关包:
- libcgroups: 默认安装, **默认子系统挂载在/sys/fs/cgroup目录**.
- libcgroup-tools.

## (5)子系统类型:
- cpuset
- cpu
- cpuacct
- memory
- devices
- freezer
- net_cls
- net_prio
- blkio
- perf_event
- hugetlb
- pids

## (6)参考:
- kernel/cgroup:代码.
- https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/6/html/resource_management_guide/ch01
- https://www.kernel.org/doc/Documentation/cgroup-v1/cgroups.txt

# 二 配置文件:
## (1)相关配置文件:
- /etc/cgconfig.conf: 用来定义cgroup以及它们的参数和挂载点, 详情man cgconfig.conf.
- /etc/cgrules.conf: 定义进程属于哪个cgroup, man cgrules.conf.
- /etc/cgconfig.d目录.

## (2)cgconfig.conf:
- 格式: 由mount,group和default三部分组成, 这些section顺序可以任意且都是可选的, 以#开头的是注释.
- mount: `mount {<controller>=<path>;...}`, controller是kernel subsystem的名字, 名字层次可以被指定作为controller(格式:name=<somename>); path是给定controller mount的目录; 若没mount指定则不会创建controller.
- group: `group <name> {[permissions] <controller> {<param name> = <param value>;...}...}`, name是control group的名字.

## (3)cgrules.conf:
- 格式: `<user>:<process name> <controllers> <destination>`
- user: 可以是一个用户名, 组名, 星号(所有用户或组), %.
- process name: 可选, 可以是一个pid或者进程的全路径cmd.
- controllers: 逗号分隔的controller names(没有空格)或星号(所有挂载的controllers).
- destination.

# 三 相关命令:
## (1)cgcreate:
- 功能: 创建cgroups.

## (2)lscgroup:
- lscgroup: 显示全部或选择的cgroups.

## (3)lssubsys:
- list hierarchies containing given subsystem.

## (4)cgdelete和cgclear:
- cgdelete [-h] [-r] [[-g] <controllers>:<path>]: 删除control groups.
- cgclear [-e] [-l <filename>] [-L <directory>] [...]: unload the cgroup filesystem.

## (5)cgconfigparser: 
- 语法: cgconfigparser [-h] [-l <filename>] [-L <directory>] [...]
- 功能: setup control group file system.

## (6)cgexec
- 语法: cgexec [-h] [-g <controllers>:<path>] [--sticky] command [arguments]
- 功能: 在指定的cgroups里运行任务.

## (7)cgget和cgset

## (8)cgsnapshot

# 四 通知:
## (1)概述:
- 通知API允许用户空间应用接收cgroup状态变化的通知, 目前只支持OOM控制文件(memory.oom_control).
