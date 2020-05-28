# 一 概述:
## (1)功能:
- 显示当前进程的信息.

## (2)常用:
- ps -elf: 查询所有进程, 标准格式.
- ps aux: 查询所有进程, bsd格式.
- ps auxf: 同上, 会显示调用路径.
- ps -eLf: 查询所有进程和线程.
- ps -ejH: 打印进程树.
- ps -T -p pid: 显示某个进程的子线程.

## (3)备注:
- pstree: 显示进程的继承树.

# 二 进程状态:
## (1)种类:
- D: Uninterruptible sleep (usually IO)
- R: Running or runnable (on run queue)
- S: Interruptible sleep (waiting for an event to complete)
- T: Stopped, either by a job control signal or because it is being traced.
- W: paging (not valid since the 2.6.xx kernel)
- X: dead (should never be seen)
- Z: Defunct ("zombie") process, terminated but not reaped by its parent.

## (2)BSD格式的额外字符:
- <: high-priority (not nice to other users)
- N: low-priority (nice to other users)
- L: has pages locked into memory (for real-time and custom IO)
- s: is a session leader
- l: is multi-threaded (using CLONE_THREAD, like NPTL pthreads do)
- +: is in the foreground process group

# 三 显示属性:
## (1)常见属性:
- PID: 进程ID.
- STAT: 进程状态.
- START: 命令启动时间, 若24小时内显示HH:MM; 超过24小时mmm dd.

## (2)显示属性的控制:
- -o/o/--format: 设置自定义的format. 例如: ps -o pid -o ppid: 显示进程id和父进程id.
- -O/O: 与-o区别:除了自定义的, 还会显示默认的几个属性.