# 一 常用配置项:
## (1)kernel.pid_max:
- PID的最大值, 当内核的下一个pid值到达pix_max时, 会从新从最小的pid分配, 进程的pid要小于pid_max的值.