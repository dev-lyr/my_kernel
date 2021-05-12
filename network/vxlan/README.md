# 一 概述:
## (1)概述:
- VXLAN: Virtual eXtensible Local Area Network.
- VXLAN is an **encapsulation** technique in which layer 2 ethernet frames are encapsulated in UDP packets
- 功能: address the need for **overlay networks** within virtualized data centers accommodating **multiple tenants**.

## (2)背景:
- 服务器虚拟化增长了对物理网络设备的需求, 一个物理机有多个有自己mac地址的虚拟机, 这就需要在链路层的交换设备有一个大的MAC地址表.
- 数据中心中的vm可以根据vlan进行分组, 当前vlan限制是4096, 同时数据中心需要支持多租户, 每个租户可能会需要独立分配mac地址和vlan id, 这就造成物理网络上存在潜在的重复的问题.
- 等等.
   
## (3)相关名词:
- VNI: vxlan network identifier(或vxlan segment id).
- VTEP: vxlan tunnel end point, vxlan tunnel的起点或终点.
- VXLAN Segment: VXLAN Layer 2 overlay network over which VMs communicate.
- VXLAN Gateway: an entity that forwards traffic between VXLANs.

## (4)备注:
- 操作: ip link
- https://tools.ietf.org/html/rfc7348
- VXLAN GPE
- Documentation/networking/vxlan.txt
- drivers/net/vxlan.c

# 二 VXLAN帧格式
## (1)概述:
- 格式: 在内部mac帧进行封装,增加四个头部(从内到外): VXLAN Header(8个字节), Outer UDP Header, Outer IP Header和Outer Etherner Head.

## (2)VXLAN Header:
- Flags(8位): 对于一个合法的VNI, I flag需设置为1, 其它7位(R)保留且发送时必须设置为0且接收时忽略.
- VXLAN Segment ID/VNI(24位): 分配给指定VXLAN overlay网络的.
- Reserved Fileds(24位和8位): 发送时设置为0,接收时忽略.

## (3)Outer UDP Header:
- 目的port: IANA分配4789作为VXLAN UDP端口,目的端口应该使用该默认值.
- 源port
- UDP Checksum

## (4)Outer IP Header:
- 源IP: 表示源VTEP的地址.
- 目的IP: 单播或多播, 当是单播时表示目的VTEP的地址.

## (5)Outer Ethernet Header:
- 帧中的outer destination MAC地址可能是目的VTEP的地址或者中间三层路由的地址.

# 三 工作方式:
## (1)概述:
- 每个overlay被称作VXLAN segment, 只有在同一个VXLAN segment的虚拟机才可以相互通信.
- 每个VXLAN segment通过一个24位的segment ID表示, 被称作VNI.
- VNI确定单个vm发起的inner MAC frame的范围, 因为可以在不同的VNI中有覆盖(overlapping)MAC地址, 不同VNI中的流量是隔离的.

# 四 VTEP:
## (1)概述:
- VXLAN Tunnel Endpoints(VXLAN隧道端点)是VXLAN网络的边缘设备, 是VXLAN隧道的起点或终点.
- VXLAN对用户原始数据帧的封装和解封装都在VTEP上进行, VTEP可以是一台独立的网络设备(交换机),也可以是服务器上虚拟交换机.
