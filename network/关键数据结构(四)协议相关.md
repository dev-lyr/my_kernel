# 一 链路层:
## (1)以太网(ethernet):
- struct ethhdr: 以太网协议头部.
- 支持协议类型: ETH_P_IP, ETH_P_ARP, ETH_P_LOOP等.
- 参考: include/linux/if_ether.h包含的include/uapi/linux/if_ether.h.

## (2)bridge.

## (3)arp:
- struct arphdr: arp协议头部.
- 参考: include/linux/if_arp.h

# 二 网络层:
## (1)ip:
- struct iphdr: ip协议头部.
- 支持协议类型: IPPROTO_TCP, IPPROTO_UDP, IPPROTO_ICMP等, 参考:include/linux/in.h.
- 参考: include/linux/ip.h.

## (2)icmp:
- struct icmphdr: icmp协议头部.
- 参考: include/linux/icmp.h

# 三 传输层:
## (1)tcp:
- struct tcphdr: tcp协议头部.
- 参考: include/linux/tcp.h.

## (2)udp
- struct udphdr: udp协议头部.
- 参考: include/linux/udp.h.