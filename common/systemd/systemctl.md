# 一 systemctl:
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
