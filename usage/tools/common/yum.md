# 一 yum： 
## (1)功能：
- 基于rpm的包管理器，自动处理依赖关系, 自动进行系统更新，安装新包，删除旧包，查询已安装或可用的包.
- 是一种高级别的包管理器，类似apt-get，yum有自己的仓库(repository).

## (2)用法：
- yum [options] [command] [package ...]

## (3)配置文件.
- /etc/yum.conf(man yum.conf)
- /etc/yum.repos.d目录：yum仓库文件存放地址.
- /var/cache/yum：缓存目录.

## (4)yum仓库(repository). 