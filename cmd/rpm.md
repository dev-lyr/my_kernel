# 一 概述：
## (1)功能：
- RPM包管理器，用来build, install, query, verify, update和erase单个软件包.
- 包：由归档文件和归档文件相关元数据(meta-data)组成.
- 包的种类：二进制包(binary packages)用来对需要安装的软件进行包装; 源码包(source packages)包含源码和产生用来产生二进制包的处方(recipe).

## (2)相关命令：
- rpmbuild：用来创建rpm包.
- rpmspec: RPM Spec Tool.

## (3)备注:
- https://rpm.org/

# 二 用法： 
## (1)查询： 
- rpm -qa：查询全部已安装packages。
- rpm -q xxx：查询指定安装包。
- rpm -qi xxx：查询指定安装包的详细信息。
- rpm -qR：查新该包依赖信息.
- rpm -ql：查询包中文件.

## (2)安装和更新：
- rpm -ivh xxx：安装软件包。
- rpm -Uvh xxx：更新软件包。

## (3)删除：
- rpm -e xxx 

# 三 rpm database 
## (1)概述：
- 每一个使用rpm安装的包都记录在RPM 数据库中，可以通过数据库查询安装了哪些包以及这些包的详细信息.
- RPM数据库在/var/lib/rpm目录下.

## (2)相关命令：
- rpm --initdb
- rpm --rebuilddb
