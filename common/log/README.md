# 一 概述：
## (1)日志系统
- syslog
- syslog-ng: syslog-next gen，https://syslog-ng.org/.
- rsyslog: https://www.rsyslog.com/
- systemd-journald服务

## (2)其它:
- dmesg
- journalctl
- logrotate命令.

## (3)

## (3)备注:
- https://tools.ietf.org/html/rfc5424


# 二 printk:
## (1)功能:
- kernel用来打印信息的函数, 类似printf.
- printk可以在内核中任何地方使用, 例如:进程上下文和中断上下文等.
- 日志level: include/linux/printk.h
- 源码: kernel/printk.c

## (2)用法:
- int printk(const char * fmt, ...)

## (3)备注:
- printk将消息保存在一个LOG_BUF_LEN大小的环形队列, 成为记录缓冲区.

# 三 重要日志文件：
##  (1)/var/log/messages：
- Contains global system messages, including the messages that are logged during system startup. There are several things that are logged in /var/log/messages including mail, cron, daemon, kern, auth, etc.

## (2)/var/log/dmesg(dmesg命令)：
- Contains kernel ring buffer information. When the system boots up, it prints number of messages on the screen that displays information about the hardware devices that the kernel detects during boot process. These messages are available in kernel ring buffer and whenever the new message comes the old message gets overwritten. You can also view the content of this file using the dmesg command.

## (3)其它：
- /var/log/auth.log：Contains system authorization information, including user logins and authentication machinsm that were used.

- /var/log/boot.log – Contains information that are logged when the system boots

- /var/log/daemon.log – Contains information logged by the various background daemons that runs on the system

- /var/log/dpkg.log – Contains information that are logged when a package is installed or removed using dpkg command

- /var/log/kern.log – Contains information logged by the kernel. Helpful for you to troubleshoot a custom-built kernel.

- /var/log/lastlog – Displays the recent login information for all the users. This is not an ascii file. You should use lastlog command to view the content of this file.

- /var/log/maillog /var/log/mail.log – Contains the log information from the mail server that is running on the system. For example, sendmail logs information about all the sent items to this file

- /var/log/user.log – Contains information about all user level logs

- /var/log/alternatives.log – Information by the update-alternatives are logged into this log file. On Ubuntu, update-alternatives maintains symbolic links determining default commands.

- /var/log/btmp – This file contains information about failed login attemps. Use the last command to view the btmp file. For example, “last -f /var/log/btmp | more”

- /var/log/cups – All printer and printing related log messages

- /var/log/anaconda.log – When you install Linux, all installation related messages are stored in this log file

- /var/log/yum.log – Contains information that are logged when a package is installed using yum

- /var/log/cron – Whenever cron daemon (or anacron) starts a cron job, it logs the information about the cron job in this file

- /var/log/secure – Contains information related to authentication and authorization privileges. For example, sshd logs all the messages here, including unsuccessful login.

- /var/log/httpd/ (or) /var/log/apache2 – Contains the apache web server access_log and error_log

- /var/log/mail/ – This subdirectory contains additional logs from your mail server. For example, sendmail stores the collected mail statistics in /var/log/mail/statistics file
