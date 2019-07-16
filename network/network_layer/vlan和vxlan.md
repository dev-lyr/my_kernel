# 一 vlan(virtual local area network):
## (1)概述:
- vlan是数据链路层的一个独立的广播域, virtual相对于lan(局域网)而言.
- vlan通过在网络包上增加和网络系统中增加tag处理来工作.
- vlan允许网络管理员将host进行分组, 即使host不在一个网络交换机下面, 大大简化网络设计和部署, 因为vlan成员关系可以通过软件配置.
- 交换机不能在vlan间转发网络流量, vlan间需通过路由器通信.