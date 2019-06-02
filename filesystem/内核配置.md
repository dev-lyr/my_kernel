# 一 相关限制:
## (1)file-max和file-nr(系统级别):
- file-max: 内核可以分配的的文件句柄(file-handle)数量.
- file-nr: 有三只值, 分别表示: 已分配的fd handles, 分配但未使用的fd handles(2.6后通常为0), 总共可以分配的fd handles.

## (2)nr_open(进程级别):
- 进程可以分配的文件句柄数量, 默认为1048576.
- 实际的使用时候依赖RLIMIT_NOFILE, 参考getrlimit和setrlimit.
- 备注: RLIMIT_NOFILE的soft limit不能大于hard limit, hard limit不能大于nr_open.