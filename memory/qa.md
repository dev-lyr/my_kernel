# 一 内存泄露

# 二 内存互踩

# 三 段错误:
## (1)现象:
- kernel: myapp[15514]: segfault at 794ef0 ip 080513b sp 794ef0 error 6 in myapp[8048000+24000]

## (2)解决方法:
- https://stackoverflow.com/questions/2179403/how-do-you-read-a-segfault-kernel-log-message/2179464#2179464

## (3)备注:
- arch/x86/mm/fault.c
