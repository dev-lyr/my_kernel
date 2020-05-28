# 一 概述： 
## (1)概念： 
- node：一个物理机.
- domain：hypervisor提供的运行在虚拟机上的一个操作系统实例.
- hypervisor：一个可以把node虚拟成多个虚拟机的软件层(layer of software).

## (2)Network:
- virtual networks：虚拟机中的网络接口.
- network interfaces：物理网络接口.

## (3)Storage：
- volume(卷)：可以分配给client作为存储卷或用来创建更深层次的pool, 卷是一个块设备、raw文件或特定格式的文件.
- Pool：提供一种管理大量存储的方法，可以把它们分为卷(volume)。可用来管理物理磁盘，NFS服务器等.

## (4)备注：
- 使用libvirt的应用：http://libvirt.org/apps.html
- virsh是libvirt对应的命令行工具.

# 二 组成部分：
## (1)libvirtd：
- The libvirtd program is the server side daemon component of the libvirt virtualization management system.
- 启动：service libvirtd start

## (2)virsh命令.

## (3)API lib库:
- 包括：c, python等. 