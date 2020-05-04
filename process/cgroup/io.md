# 一 概述:
## (1)子系统:
- **blkio**: 实现block io控制器, 提供丰富的IO控制策略.
- **devices**: Implement a cgroup to track and enforce open and mknod restrictions on device files.

## (2)配置选项:
- CONFIG_BLK_CGROUP
- CONFIG_BLK_DEV_THROTTLING
- CONFIG_DEBUG_BLK_CGROUP

# 二 blkio策略文件:
## (1)类型:
- proportional weight policy file
- throttling/upper limit policy file

## (2)比例权重:
- blkio.weight: 指定每个cgroup的权重, 是每个cgroup在所有device上的默认权重, 除非没每个device的规则覆盖(blkio.weight_device), 可选范围:10-1000.
- blkio.weight_device: 指定每个cgroup在指定device上的权重.
- 等等.

## (3)限流:
- blkio.throttle.read_bps_device 
- blkio.throttle.write_bps_device
- blkio.throttle.read_iops_device
- blkio.throttle.write_iops_device
