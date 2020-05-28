# 一 概述： 
## (1)功能：
- QEMU是一个仿真器(emulator)和虚拟化技术.
- QEMU是动态翻译(portable dynamic translator)，遇到一段code时，将它转换为机器指令.

## (2)参考：
- https://www.qemu.org/
- http://qemu.weilnetz.de/qemu-doc.html

## (3)相关命令：
- qemu-kvm/qemu-system-x86_64/qemu-system-i386
- qemu-img：QEMU disk image utility.
- qemu-io：QEMU Disk exerciser.
- qemu-nbd：QEMU Disk Network Block Device Server.

# 二 操作模式：
## (1)全系统仿真(Full system emulation).
- QEMU仿真一个完整系统，包括处理器和其它外部设备.
- 可以启动不同的OS.

## (2)用户模式仿真(User mode emulation).
- launch processes compiled for one CPU on another CPU, however the Operating Systems must match.