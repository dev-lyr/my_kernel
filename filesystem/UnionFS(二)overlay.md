# 一 概述:
## (1)概述:
- 一个overlay文件系统包含两个文件系统: **upper**文件系统和**lower**文件系统, 当一个名字出现在两个文件系统中时, lower文件系统的文件会被隐藏.
- lower文件系统可以是任意linux支持的文件系统且不需要是可写的.
- upper文件系统是可写的.

## (2)备注:
- Documentation/filesystems/overlayfs.txt