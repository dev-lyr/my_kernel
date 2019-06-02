# 一 概述:
## (1)功能:
- 内核用于通知用户空间程序文件系统变化.
- man inotify
- Documentation/filesystems/inotify.txt

## (2)相关API:
- inotify_init: 创建一个inotify实例并且返回关联该inotify实例的文件描述符fd.
- inotify_add_watch: 操控给定inotify实例的监测列表(watch list).
- inotify_rm_watch: 从监测列表删除一个监测项(watch).

## (3)用途:
- 日志抓取等.