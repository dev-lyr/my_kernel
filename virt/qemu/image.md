# 一 qemu支持镜像类型： 
## (1)raw(默认)：
- 简单、容易移植到其它仿真器(emulators).
- 使用的空间大小就是镜像中存储数据的大小.

## (2)qcow和qcow2：
- qcow：旧qemu镜像格式.
- qcow2：qemu镜像格式，最通用的格式.

## (3)其它：
- cloop
- cow
- vmdk：VMware3和4兼容镜像模式.
- vdi：VirtualBox
- vhdx
- vpc/vhd：VirtualPc兼容镜像格式.

## (4)备注：
- https://en.wikibooks.org/wiki/QEMU/Images

# 二 qemu-img命令： 
## (1)功能： 
- 线下创建、转换和修改镜像，可以处理所有qemu支持的镜像类型.
- 注意不要修改正在运行虚拟机使用的镜像，会损坏镜像.
- 用法: qemu-img command [command options].

## (2)常用子命令：
- info
- create
- convert
- snapshot