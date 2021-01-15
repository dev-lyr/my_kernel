# 一 概述:
## (1)功能:
- systemd-journald是一个用来收集和存储日志数据的系统服务.
- 创建和维护结构化,可索引日志数据, 可接收多种日志数据源.
- 默认,journal将日志数据存储到/run/log/journal, 因为/run是变化的, 当机器重启时日志数据会丢失.
- 若需持久化, 需创建/var/log/jounal/目录来存储日志数据.

## (2)日志数据源:
- kernel日志信息, 通过kmsg.
- 简单系统日志信息, 通过syslog调用.
- 结构化系统日志信息, 通过native journal API.
- 系统服务的stdout和stderr.
- Audit记录, 通过Audit系统.

## (3)相关:
- systemd-journald服务: /usr/lib/systemd/systemd-journald
- systemd-journald.socket
- journalctl命令.

## (4)备注:
- man systemd-journald.service

# 二 journalctl命令:
## (1)功能:
- 查询systemd-journald服务写入的systemd日志内容.
- 语法: `journalctl [OPTIONS...] [MATCHES...]`

## (2)选项:
- -u, --unit=UNIT|PATTERN: 只显示指定UNIT或者UNIT匹配PATTERN的unit的日志.
- -f: 只显示最新的日志以及后续新增的日志.

## (3)MATCHES:
- 备注: man systemd.journal-fields

# 三 配置:
## (1)概述:
- man journald.conf

## (2)日志转发:
- ForwardToSyslog
- ForwardToKMsg
- ForwardToConsole
- ForwardToWall
- 备注: Control whether log messages received by the journal daemon shall be forwarded to a traditional syslog daemon, to the kernel log buffer (kmsg), to the system console, or sent as wall messages to all logged-in users.

