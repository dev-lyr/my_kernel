# 一 概述:
## (1)介绍.

## (2)相关工具:
- ethtool: query or control network driver and hardware settings.
- ifconfig

# 二 相关属性:
## (1)offload属性(ethool -k xxx):
- rx on/off: 设置是否开启RX检验和(checksumming).
- tx on/off: 设置是否开启TX检验和.
- sg on/off: 设置是否开启分散/聚集(Scatter/Gather)功能.
- tso(tcp segmentation offload) on/off: 设置是否开启tcp分片offload功能, 允许网卡将单个frame分片为多个frame, 减轻cpu负载, 依赖tx检验和.
- uso(udp segmentation offload) on/off: 设置是否开启udp分片offload功能.
- gso(general segmentation offload) on/off: 设置是否开启通用分片offload功能.
- gro(general receive offload) on/off: 设置是否开启通用接收分片offload功能.
- 备注: 内核文档Documentation/networking/segmentation-offloads.txt
