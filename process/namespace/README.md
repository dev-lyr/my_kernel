# 一 NameSpaces：
## (1)功能：
- 对全局系统资源进行包装和抽象, 使得一个在命令空间里进程拥有自己独立的全局资源实例.
- 对命名空间里全局资源的改变, 对其它命名空间里的进程是不可见的.
- 提供一种资源隔离方案:PID,IPC,Network等系统资源不再是全局的,而是属于特定的Namespace的.
- 用来实现容器(docker).

## (2)NameSpaces种类：
- IPC命名空间(CLONE_NEWIPC)：System V IPC, POSIX message queues，IPC隔离后只有在一个namespace的进程才能通信.
- Network命名空间(CLONE_NEWNET)：Network devices, stacks, ports,etc.
- Mount命名空间(CLONE_NEWNS)：Mount points.
- PID命名空间(CLONE_NEWPID)：Process IDs.
- User命名空间(ClONE_NEWUSER)：User and group IDs.
- UTS命名空间(CLONE_NEWUTS)：Hostname and NIS domain name.
- CGROUP命名空间(CLONE_CGROUP): new cgroup namespace.

## (3)备注:
- 文档: Documentation/namespaces.
- /proc/pid/ns.

# 二 相关API：
## (1)clone：
- clone创建进程时，若flags字段指定上面的`CLONE_NEW*`，则会创建指定的namespaces，并且这个进程会成为这些namespaces的成员.
- 从内核2.6版本才有.

## (2)setns：
- 把调用进程添加到已存在的namespace.
- /proc/[pid]/ns/xxx：进程加入指定namespace，则会在该目录下有一个对应的namespace的子目录.

## (3)unshare：
- 把调用进程移动到一个新的namespace.
