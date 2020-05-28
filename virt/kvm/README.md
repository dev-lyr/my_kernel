# 一 概述：
## (1)相关概念：
- KVM: Kernel-based Virtual Machine，全虚拟化解决方案，适用于linux x86硬件包含Intel VT或AMD-V扩展.
- kvm是集成到linux内核的hypervisor，使用两个内核模块kvm.ko和kvm_intel.ko(或kvm_amd.ko).
- 每个vm都是linux中一个常规的**进程**, 被kernel标准调度器调度, 拥有专有的虚拟硬件, 比如:网卡,CPU,内存和磁盘等.
- kvm自己不执行任何仿真，暴露一个/dev/kvm接口给用户空间工具qemu，虚拟机就是linux中的一个普通进程. QEMU运行在用户空间, kvm运行在内核空间, qemu通过ioctl与kvm进行交互.
- 可以直接运行未修改的linux或windows镜像，每个虚拟机有自己的虚拟化硬件：网卡、磁盘等.

## (2)相关工具：
- qemu-kvm：用户在kvm上操作还需要一个用户空间工具，kvm对qemu做了一定的修改，形成了自己的kvm虚拟机工具集和IO虚拟化的支持，即qemu-kvm，Qemu1.3已经完整支持all qemu-kvm特性.
- KVM只是一个内核模块，没有用户空间管理工具，需借助QEMU来管理；同样QEMU是纯软件模拟，比较慢，可以借助kvm来加速提升虚拟机的性能.
- libvirt：调用kvm和xen等虚拟化技术的接口用于执行相关操作，直接用qemu-kvm接口太繁琐。

## (3)备注：
- http://www.linux-kvm.org/page/Main_Page.
- http://wiki.qemu.org/Manual.
- https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/?version=7
- 判断CPU是否支持kvm：grep vmx /proc/cpuinfo(Intel)；grep svm /proc/cpuinfo(AMD).
- 源码：linux源码中带有，virt/kvm目录.