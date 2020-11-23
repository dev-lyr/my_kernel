# 一 du
# 二 df
# 三 dd:
## (1)功能:
- 复制, 转换和格式化文件.

## (2)语法:
- dd [OPERAND]
- dd OPTION

## (3)常用选项:
- if=xx: 从xx文件读取代替标准输入.
- of=xx: 写入xx文件代替标准输出.
- bs=xx: 设置ibs和obs.
- ibs=xx: 一次读取的字节数, 即block的大小.
- obs=xx: 一次写入的字节数, 即block的大小.
- count=xx: 只读取xx个blocks.

## (4)常用:
- dd if=/dev/zero of=/dev/null

# 四 lsof
