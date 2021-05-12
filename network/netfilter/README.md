# 一 概述:
## (1)功能:
- 包过滤: 有状态和无状态的包过滤.
- NAT/NAPT: 所有类型的网络地址和端口translation.
- do further packet manipulation (mangling) like altering the TOS/DSCP/ECN bits of the IP header.
- 等等.

## (2)组成:
- **netfilter**: 由内核中一系列**hook**组成, hook允许内核模块在网络协议栈注册callback函数, 当每个包穿过(traverse)对应网络协议栈中的对应hook时callback函数会被调用.
- **iptables**: 一个用于定义rulesets的表结构.
- **connection tracking**
- **NAT子系统**

## (3)相关命令:
- iptables
- ebtables
- arptables
- nftables: 用来替换{ip,ip6,arp,eb}tables

## (4)备注:
- /proc/sys/net/netfilter/
- https://www.netfilter.org/documentation/index.html
- https://www.netfilter.org/documentation/HOWTO/netfilter-hacking-HOWTO.html
- 架构图: https://www.netfilter.org/documentation/HOWTO/netfilter-hacking-HOWTO-3.html

# 二 Hook:
## (1)概述:
- 不同协议类型的Hook点类型不一样.

## (2)Hook支持的协议类型:
- NFPROTO_UNSPEC =  0
- NFPROTO_INET   =  1
- NFPROTO_IPV4   =  2
- NFPROTO_ARP    =  3
- NFPROTO_NETDEV =  5
- NFPROTO_BRIDGE =  7
- NFPROTO_IPV6   = 10
- NFPROTO_DECNET = 12
- NFPROTO_NUMPROTO

## (3)INET的Hook点类型(enum nf_inet_hooks):
- NF_INET_PRE_ROUTING: 进方向, 路由之前.
- NF_INET_LOCAL_IN: 进方向, 路由之后发现是本地.
- NF_INET_FORWARD: 进方向, 路由之后发现是其它接口, 需要转发.
- NF_INET_LOCAL_OUT: 出方向, 本地产生包, 路由之前.
- NF_INET_POST_ROUTING: 进方向NF_INET_FORWARD之后; 出方向在NF_INET_LOCAL_OUT之后的路由后.
- NE_INET_NUMHOOK
- 适用于: NFPROTO_INET, NFPROTO_IPV4和NFPROTO_IPV6.

## (4)NFPROTO_BRIDGE的Hook点类型:
- NF_BR_PRE_ROUTING
- NF_BR_LOCAL_IN		
- NF_BR_FORWARD		
- NF_BR_LOCAL_OUT		
- NF_BR_POST_ROUTING	
- NF_BR_BROUTING		
- NF_BR_NUMHOOKS		
- 参见: include/uapi/linux/netfilter_bridge.h

## (5)NFPROTO_ARP的Hook点类型:
- NF_ARP_IN
- NF_ARP_OUT
- NF_ARP_FORWARD
- NF_ARP_NUMHOOKS
- 参见: include/uapi/linux/netfilter_arp.h

## (6)全局变量:
- hooks[NFPROTO_NUMPROTO][NF_MAX_HOOKS]:各种协议类型的注册的hook的集合, 参考:include/net/netns/netfilter.h

## (7)备注:
- include/linux/netfilter.h
- net/netfilter.

# 三 Hook结构:
## (1)struct nf_hook_ops(表示一个Hook):
- struct list_head list
- hook: hook的callback函数.
- int priority: 优先级.
- unsigned int hooknum
- u_int8_t pf: 协议.

## (2)Hook的注册和卸载:
- nf_register_hook和nf_register_hooks
- nf_unregister_hook和nf_unregister_hooks

## (3)Hook的状态(struct nf_hook_state).

# 四 Hook的调用:
## (1)调用时机和方式:
- 在包穿过Hook点时候被调用, 方式为执行**NF_HOOK函数**.

## (2)NF_HOOK(pf, hook ... okfn):
- 调用该函数执行相应协议的相应hook点的hook函数, 并在hook返回后执行okfn函数.

## (3)Hook函数的返回:
- NF_DROP 0: 丢掉报文, 并释放skb.
- NF_ACCEPT 1: 表示该hook函数允许报文继续执行该队列上的下一个hook函数, 前一个通过并不能返回, 需要所有的执行完并且为NF_ACCPET时才能返回NF_ACCEPT, 参考nf_iterate函数的实现, 继续往下走, 会调用okfn.
- NF_STOLEN 2: 包由队列上的所有hook函数执行, 不会再继续传递.
- NF_QUEUE 3: 对包进行排队, 通常由用户空间处理.
- NF_REPEAT 4: 重复执行一次当前的hook函数.
- NF_STOP 5: 停止执行该队列上的hook函数, 继续往下走, 会调用okfn.
- NF_MAX_VERDICT NF_STOP
