# 一 概述:
## (1)概述:
- veth(virtual ethernet device)
- veth设备是虚拟设备.

## (2)功能:
- act as **tunnels between network namespaces** to create a bridge to a physical network device in **another namespace**.
- used as standalone network devices.

## (3)备注:
- man veth(4)

# 二 veth pair:
## (1)概述:
- veth设备通常以interconnected pairs形式被创建.
- Packets transmitted on one device in the pair are immediately received on the other device.

## (2)使用:
- 创建: ip link add <p1-name> type veth peer name <p2-name>
- 查询peer: ethtool -S p1-name显示的peer_ifindex.
