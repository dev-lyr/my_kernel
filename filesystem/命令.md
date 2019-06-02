# 一 mkfs：
## (1)功能:
- 功能：在设备上创建文件系统，通常是硬盘分区.

## (2)用法:
- mkfs [ -V ] [ -t fstype ] [ fs-options ] filesys [ blocks ]
- filesys：设备名字，例如：/dev/sda1, /dev/sda2等.
- blocks：文件系统使用的块的总数.
- -t fstype：设置创建的文件系统的类型，默认是系统默认的文件系统类型.

# 二 mount:
## (1)功能:
- Unix系统中所有可访问的文件都以一棵大文件树的形式呈现, root为/.
- mount命令将一些device上发现的文件系统attach到这个大文件树.

## (2)用法:
- mount [-lhv]
- mount -a [-fFnrsvw] [-t vfstype] [-O optlist]
- mount [-fnrsvw] [-o option[,option]...]  device|dir
- mount [-fnrsvw] [-t vfstype] [-o options] device dir

## (3)选项:
- -a,--all: 挂载fstab中所有文件系统.
- -t,--types vsftype: 指定文件系统类型.
- -l, --show-labels: 在mount的输出中添加lables.
- -o,--options opts: 参考(4)和(5).

## (4)文件系统中立选项

## (5)文件系统相关选项