# 一 概述:
## (1)概述:
- man resolver

# 二 常用文件:
## (1)/etc/hosts:
- the static lookup for hostnames(man 5 hosts).
- 功能: 把主机名映射到IP地址，只包含本地映射关系，最好用它保存系统引导时所需的映射关系(例如主机自身、默认网关和名字服务器的映射关系)，使用DNS或LDAP来找到本地网络与外界的映射关系.
- 格式: ip_address canonical_hostname [aliases...别名]，每行以IP地址开头，后面跟着主机名，通常把localhost放在第一行.
- 注意: 通常linux主机查询对方身份时，首先查询/etc/hosts文件的设置，接下来是/etc/resolv.conf的DNS主机.

## (2)/etc/hostname(或/etc/sysconfig/network):
- 设置机主名, 相关命令hostname.
- 用来在局域网内表示机器,映射到IP类似domain name.

## (3)/etc/resolv.conf:
- resolver configuration file(man 5 resolv.conf).
- 功能: DNS客户机的配置文件，用于设置DNS服务器的IP地址以及DNS域名、主机的域名搜索顺序，该文件是**域名解析器**(resolver)使用的配置文件.
- 格式: nameserver ip, 除了nameserver还包含：domain、search和sortlist等配置选项.
- 注意: 如果主机通过DHCP获得其DNS服务器地址，则不需手动配置这个文件.

## (4)/etc/host.conf:
- resolver configuration file(man 5 host.conf).
- 功能: order关键字用来指定主机名解析顺序，通常是先/etc/hosts文件，再搜bind名字服务器(DNS); multi关键字：是否允许主机有多个ip地址，on或者off，默认为off; nospoof：是否禁止IP欺骗，on或者off，默认为off.
