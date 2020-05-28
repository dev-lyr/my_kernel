# 一 概述：
## (1)功能：
- kvm中主要的IO虚拟化平台，参考:http://www.linux-kvm.org/page/Virtio.

## (2)相关技术:
- vhost-net: 是传统virtio net的优化, 在kernel中实现virtio net.
- vhost-user: dpdk等.
- SR-IOV

# 二 架构：
## (1)组成：
- 前端驱动程序(client系统中实现).
- 支持client到hypervisor通信的virtio和virtio_ring.
- 后端驱动程序(hypervisor(kvm)中实现).

## (2)client系统中的virtio driver：
- virtio-blk：drivers/block/virtio_blk.c
- virtio-net：drivers/net/virtio_net.c
- virtio-pci：drivers/virtio/virtio_pci.c
- virtio-ballon：drivers/virtio/virtio_balloon.c
- virtio-console：drivers/virtio/virtio_console.c

## (3)中间层：
- virtio：drivers/virtio/virtio.c
- transport(virtio-ring)：driver/virtio/virtio_ring.c
