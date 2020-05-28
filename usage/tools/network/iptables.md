# 一 概述
## (1)功能:
- iptables/ip6tables: IPv4/IPv6的包过滤和NAT管理工具.
- 语法: `类似iptables [-t table] {-A|-C|-D} chain rule-specification`

## (2)常用选项:
- `-t,--table table`: 指定对应执行操作命令的表, 默认为filter表.
- `-L,--list [chain]`: 查询指定chain的规则,若没指定chain则显示所有chain.
- `-S,--list-rules [chain]`: 查询指定chain的规则, 若没指定chain则以iptables-save形式显示所有规则.
- `-A,--append chain rule-specification`: 添加一个或多个规则到指定的链的尾部.
- `-I,--insert chain [rulenum] rule-specification`: 向指定链中的指定num插入规则,若不指定rulenum, 则默认为1, 即查到链的头部.
- `-R,--replace chain rulenum rule-specification`: 替换指定链中的指定num的规则.
- `-D,--delete chain rule-specification/rulenum`: 从指定链中删除规则. 
- `-F,--flush [chain]`: 刷新指定的chain, 若没有指定chain则刷新所有chain, 类似于删除所有规则.
- `-N,--new-chain chain`: 创建一个**自定义链**.
- `-X,--delete-chain [chain]`: 删除自定义链.
- `-E,--rename-chain old-chain new-chain`: 修改链的名字.
- `-P,--policy chain target`: 设置chain的target, 只有build-in链可以有target.


## (3)rule：
- rule-specification = [matches...] [target] 
- match = -m matchname [per-match-options] 
- target = -j targetname [per-target-options]
- 参数: man iptables

## (4)target：
- ACCEPT：let the packet through.
- DROP：drop the packet on the floor.
- QUEUE：pass the packets to userspace.
- RETURN：stop traversing this chain  and  resume at  the  next  rule in the previous (calling) chain. If the end of a built-in chain is reached or a rule in a built-in chain with target RETURN is matched, the target specified by the chain policy determines the fate of the packet.
- 自定义链
- 备注: A firewall rule specifies criteria for a packet and a target.If the packet does not match, the next rule in the chain is examined; if it does match,then the next rule is specified by the value of the target, which can be the name of a **user-defined chain, one of the targets described in iptables-extensions(8),or one of the special values ACCEPT,DROP or RETURN.**

## (5)备注:
- 其它: arptables, ipv6tables, ebtables
- nftables: 新版本, 用来替代xxtables, 3.13以后可用, 参考https://www.netfilter.org/projects/nftables.

# 二 表的类型:
## (1)filter表:
- INPUT链：packets destined to local sockets, 对应 NF_INET_LOCAL_IN的hook点.
- FORWARD链：packets being routed through the box, 对应NF_INET_FORWARD的hook点.
- OUTPUT链：locally-generated packets, 对应NF_INET_LOCAL_OUT的hook点.

## (2)nat表:
- PREROUTING链: 包进来时候就修改, 对应NF_INET_PRE_ROUTING hook点.
- OUTPUT链：本地产生的包, 在路由之前修改, 对应NF_INET_LOCAL_OUT的hook点.
- POSTROUTING链：在包即将发出去时候修改, 对应NF_INET_POST_ROUTING的hook点.

## (3)mangle表.

## (4)raw表.

## (5)security表.

# 三 rule规范:
## (1)相关参数:
- `-4,--ipv4`
- `-6,--ipv6`
- `[!] -p,--protocol protocol`: rule的协议, 可以是tcp,udp,icmp等等, 协议名字参考/etc/protocols, all代表所有协议, all是默认值, 其中数字0等同于all. 可以通过!进行取反.
- `[!] -s,--source address[/mask][,..
- `[!] -d,--destination address[/mask][,...]`: 目的地址.
- `-m,--match match`: 指定一个match, 一个用来测试指定属性的扩展模块.
- `-j,--jump target`: 指定rule的target, 指定当rule match时需做什么, target可以是: 用户自定义的chain, 内置的target或一个扩展.
- `-g, --goto chain`.
