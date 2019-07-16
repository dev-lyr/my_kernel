# 一 常用概念:
## (1)局域网(local area network)相关：
- **vlan(virtual local area network)**: 局域网网段构成的与物理位置无关的逻辑组，属于同一网段的一组端口，这些网段具有共同需求; 每个vlan的帧都有一个标示符，指示该帧属于哪个vlan。交换机不向vlan之外的工作站发生广播信息，不同vlan间的通信需要路由器，可以避免广播风暴; 相关目录：/proc/net/vlan.

- **vxlan(virtual extensible lan)**.

## (2)广域网(wide area network)相关.

# 二 常用文件:
## (1)/etc/hosts:
- the static lookup for hostnames(man 5 hosts).
- 功能: 把主机名映射到IP地址，只包含本地映射关系，最好用它保存系统引导时所需的映射关系(例如主机自身、默认网关和名字服务器的映射关系)，使用DNS或LDAP来找到本地网络与外界的映射关系。
- 格式: ip_address canonical_hostname [aliases...别名]，每行以IP地址开头，后面跟着主机名，通常把localhost放在第一行。
- 注意: 通常linux主机查询对方身份时，首先查询/etc/hosts文件的设置，接下来是/etc/resolv.conf的DNS主机。

## (2)/etc/hostname(或/etc/sysconfig/network):
- 设置机主名, 相关命令hostname.
- 用来在局域网内表示机器,映射到IP类似domain name.

## (3)/etc/resolv.conf:
- resolver configuration file(man 5 resolv.conf)。
- 功能: DNS客户机的配置文件，用于设置DNS服务器的IP地址以及DNS域名、主机的域名搜索顺序，该文件是**域名解析器**(resolver)使用的配置文件。
- 格式: nameserver ip。除了nameserver还包含：domain、search和sortlist等配置选项。最多可以由3个nameserver项。
- 注意: 如果主机通过DHCP获得其DNS服务器地址，则不需手动配置这个文件。

## (4)/etc/host.conf:
- resolver configuration file(man 5 host.conf)。
- 功能: order关键字用来指定主机名解析顺序，通常是先/etc/hosts文件，再搜bind名字服务器(DNS); multi关键字：是否允许主机有多个ip地址，on或者off，默认为off; nospoof：是否禁止IP欺骗，on或者off，默认为off.

## (5)/etc/services:
- Internet network services list(man 5 services)。
- 功能: 该文件定义了系统中标准网络服务对应的端口和协议类型，存在的服务条目不代表当前正在运行于机器上。
- 主要: 很多系统程序需使用该文件，一般情况不要修改该文件，因为这些设置都是Internet标准的设置。

# 三 链路层(link layer)相关:
## (1) 交换机相关:
- **未知单播**: 交换机初始时，mac地址是空的，此时A发生一个帧到B，那么交换机接收到此帧时候，查看源地址## (主机A)，并将它添加到MAC地址表，但是交换机不知道B在哪个端口(mac地址表中没有B的MAC地址)，所以这个帧就是未知单播帧，交换机会flooding这个帧。
- **广播和多播**: 当网桥收到一个目的地址是链路层广播或多播地址的帧时，会将该帧复制给每个端口## (接收该帧的端口除外)。
- **定时器**: 为了让网桥能适应拓扑的变化，网桥为每个地址项设定了一个定时器，当首次学到该地址时，定时器就启动，以后任何时候再次监听到该主机时，就重启定时器，以便确认和更新地址,默认的老化时间是5分钟.
- **Bridge flooding**: 若数据帧中的目的地址不在交换机的MAC地址表中，则向所有端口转发.

## (2)网卡相关:
- **网卡绑定(bonding)**: 将多个网卡绑定成单个逻辑网卡, 通过负载平衡来提高数据吞吐量, 提高了冗余性, 允许单个设备故障.

# 四 网络层(network layer)相关

# 五 传输层(transport layer)
