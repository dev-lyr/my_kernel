# 一 概述:
## (1)功能:
- systemd是一个Linux上的系统和服务管理者, 在系统boot时候作为一个进程执行(pid为1), 作为init系统拉起和维护用户空间服务.

## (2)配置文件:
- 默认systemd配置文件为:/etc/systemd/system.conf.
- man systemd-system.conf

## (3)相关命令:
- systemctl
- systemd
- journalctl

## (4)相关:
- SysV init系统:需要在系统启动时启动的服务需在/etc/rc数字.d下建立一个到/etc/init.d/xxx下服务执行脚本的软连接; /etc/init.d/xxx: 存放服务端启动脚本, 支持service操作.
- supervisor: http://supervisord.org/

## (5)备注:
- https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/7/html/system_administrators_guide/index

# 二 systemd units:
## (1)概述:
- systemd引入了systemd units概念, 这些units通过unit配置文件来表示, 封装了关于系统服务, 监听套接字和其它与init 系统相关对象的信息.

## (2)unit类型:
- **Service unit(.service)**: A system service, 以前系统版本/etc/rc.d/init.d/下的init脚本被service unit替代.
- **Target unit(.target)**: A group of systemd units.
- **Automount unit(.automount)**: A file system automount point.
- **Device unit(.device)**: A device file recognized by the kernel.
- **Mount unit(.mount)**: A file system mount point.
- **Path unit(.path)**: A file or directory in a file system.
- **Scope unit(.scope)**: An externally created process.
- **Slice unit(.slice)**: A group of hierarchically organized units that manage system processes.
- **Snapshot unit(.snapshot)**: A saved state of the systemd manager.
- **Socket unit(.socket)**: An inter-process communication socket.
- **Swap unit(.swap)**: A swap device or a swap file.
- **Timer unit(.timer)**: A systemd timer.

## (3)unit文件目录:
- **/usr/lib/systemd/system/**: Systemd unit files distributed with installed RPM packages.
- **/run/systemd/system/**: Systemd unit files created at run time. This directory takes precedence over the directory with installed service unit files.
- **/etc/systemd/system/**: Systemd unit files created by systemctl enable as well as unit files added for extending a service. This directory takes precedence over the directory with runtime unit files.

# 三 systemctl:
## (1)概述:
- 控制systemd系统的状态和service manager.
- 用法: systemctl [选项] COMMAND [NAME]

## (2)常用选项:
- -a,--all: 显示所有loaded的unit, 不管状态(即是不是active).
- -t,--type=: 参数为逗号分裂的unit类型列表.
- --state=: 参数是逗号分隔unit LOAD, SUB或ACTIVE状态.

## (3)命令:
- Unit命令: list-units, list-sockets, start, stop, status, reload, kill等.
- Unit文件命令: list-unit-files
- System命令: default, rescue, reboot, halt, suspend等.
- Machine命令: list-machines
- Job命令: list-jobs, cancel
- Snapshot命令: snapshot, delete.
- Environment命令: show-environment, set-environment
