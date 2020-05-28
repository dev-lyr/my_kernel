# 一 vlan(virtual local area network):
## (1)概述:
- vlan是数据链路层的一个独立的广播域, virtual相对于lan(局域网)而言.
- vlan允许网络管理员将host进行分组, 即使**host不在一个网络交换机下面**, 大大简化网络设计和部署, 因为vlan成员关系可以通过软件配置.
- 交换机不能在vlan间转发网络流量, vlan间需通过**路由器**通信.

## (2)功能:
- 限制广播风暴.
- 增强局域网安全性.
- 灵活性: vlan可将不用地点,不同网络的机器组合在一起, 形成一个虚拟的局域网环境.

## (3)通信类型:
- 同一交换机下同一vlan内机器通信.
- 不同交换机下同一vlan内机器通信.
- 不同vlan间机器通信.

## (4)缺陷:
- VLAN ID是12位, 因此最多有4096个VLAN. 
- VLAN不适用于多租户.
- VLAN使用STP.

## (5)备注:
- https://tools.ietf.org/html/rfc3069
- https://en.wikipedia.org/wiki/IEEE_802.1Q
