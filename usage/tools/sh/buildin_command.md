# 一 概述:
## (1)概述:
- 内置命令是包含在shell内部, shell直接执行这些命令, 无需调用其它程序.

# 二 常用:
## (1) .和source filename [arguments]:
- 在当前shell环境读取和执行filename, 返回最后一个命令的执行状态.
- 与bash和./filename区别: source是在当前进程环境, 而bash会创建新的进程.

# 三 变量相关:
## (1)env
- 格式：env [-i] [var=value ... ] [command_name [ arguments ...]]

## (2)export

## (3)set和unset
