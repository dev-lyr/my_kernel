# 一 概述：
## (1)linux系统的errno码：
- /usr/include/asm-generic/errno.h
- /usr/include/asm-generic/errno-base.h

## (2)perror命令:
- 可查错误码数字对应的字符串.

## (3)errno变量:
- 每个线程有自己局部error变量，互不干扰。
- 若没有出错，errno的值不会清除.
- 任一函数都不会将errno的值设为0，因为在errno.h定义的所有错误常量都不为0.

# 二 相关函数:
## (1)error.h
- `error`
- `error_at_line`

## (2)c标准提供:
- `perror(const char *msg)`: 基于当前errno的值，在标准错误上产生一条出错信息，格式为：msg: errno对应的出错信息.
- `strerror`: 将errno映射为一个字符串表示.
