# 一 概述:
## (1)概述:
- Linux标准的可执行格式是ELF(Executable and Linking Format).
- Linux支持其他不同格式的执行文件, 能运行为其他系统编译的程序.
- Linux允许用户注册自定义的可执行格式, 内核确定可执行文件时自定义格式时, 就启动对应的解释程序.

## (2)linux_binfmt:
- 可执行格式由类型为Linux_binfmt的对象来描述, 所有的linux_binfmt对象处于一个单项链表中, 可通过register_binfmt和unregister_binfmt函数在链表中插入和删除元素.
- 当系统启动时, 每个编译进内核的可执行格式都执行register_binfmt函数.
- 链表中最后一个元素总是"解释脚本"的可执行格式, 检查可执行文件是否已#!字符开始, 若是则把第一行其余部分解释为一个可执行文件的路径名, 并把脚本名作为参数传递以执行它.
