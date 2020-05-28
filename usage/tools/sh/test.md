# 一 test:
## (1)功能:
- 测试表达式的退出码.
- test用来测试文件属性、比较字符串及比较数字.

## (2)语法(man test):
- test expression
- [ expression ]

## (3)退出码:
- 每一条命令，不管是内置、Shell函数，还是外部的，当它退出时，都会返回一个小的整数值给引用它的程序，即退出状态.
- 退出状态为0表示“成功”；其他任何退出状态都为失败. 内置变量“#?”包括了Shell最后一次执行的一个程序的退出状态.

# 二 expression:
## (1)常用:
<pre><code>
-f file: file是一般文件.
-h/L file: file是符号链接.
-p file: file是管道
-S file: file是socket.
-r file: file是可读的.
-w file: file是可写的.
-x file: file是可执行的.
-s file: file不是空的.
-n string: string是非null.
s1 = s2: 字符串s1等于s2
s1 != s2: 字符串s1不等于s2
n1 -eq n2: 整数n1等于n2
n1 -ne n2: 整数n1不等于n2
</pre></code>
