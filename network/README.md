# 一 概述:
## (1)包发送和接收方案:
- kernel内置协议栈
- bypass kernel, 例如:dpdk.
- rdma

## (2)流量方向:
- 接收: L1->L2->L3->L4->L5.
- 发送: L5->L4->L3->L2->L1
- 转发: L1->L2(bridge)->L1或L1->L2->L3(路由)->L2->L1.



