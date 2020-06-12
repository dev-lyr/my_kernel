# 一 概述:
## (1)类型:
- 文件存储: NAS,NFS,HDFS等, 常用于共享存储.
- 块存储: SAN等.
- 对象存储: Ceph, Swift, OSS, Amazon S3等.

## (2)相关概念:
- NAS(Network Attached Storage)
- SAN(Storage Area Network)
- OBS(Object-Based storage)

## (3)相关系统:
- NFS
- HDFS
- Ceph
- glusterfs

## (4)对比

## (5)备注:
- https://www.redhat.com/zh/topics/data-storage/file-block-object-storage

# 二 对象存储:
## (1)概述:
- 基于对象的存储, 是一种扁平结构, 文件被拆分为多个部分并分散在多个硬件间.
- 在对象存储中, 数据被分解为被称为对象的离散单元, 并保存在单个存储库中.
- 对象的大小不固定.

## (2)协议

## (3)优缺点:
- 优点: 可以轻松扩展, 是公有云存储首选; 适用于静态数据的存储, 且擅长存储非结构化数据.
- 缺点: 不支持修改对象, 只能一次全部写入.

# 三 块存储:
## (1)概述:
- 块大小固定.

## (2)协议


# 四 文件存储:
## (1)概述

## (2)协议

