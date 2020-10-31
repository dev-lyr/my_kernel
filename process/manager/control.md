# 一 prctl:
## (1)功能:
- 操作一个进程, 查询和修改各种配置等功能.

## (2)格式:
- `int prctl(int option, unsigned long arg2, unsigned long arg3, unsigned long arg4, unsigned long arg5)`

## (3)option:
- PR_SET_CHILD_SUBREAPER: 若arg2不为0, 则设置调用进程的"child subreaper"属性, 所有它的后继进程会被标记有一个subreaper, 效果就是当前进程对它的后继进程履行init的角色, 例如: 若某个孙子的父进程跪了, 该进程会变成该孙子进程的新的父进程而不是init进程.
