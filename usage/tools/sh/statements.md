# 一 if语句:
## (1)语法:
<pre><code>
if pipeline [pipeline ...]
then
statements-if-true-1
[elif pipeline] [pipeline ...]
then
statements-if-true-2
[else
statements-if-all-else-fails]
fi
</code></pre>

## (2)逻辑的NOT,AND与OR:
- NOT: ！
- AND: &&
- OR: ||

# 二 case语句:
## (1)语法:
<pre><code>
case expression in
pattern1)
statements;;
pattern2)
statements;;
pattern3 | pattern4
statements;;
*)
statements;;
</code></pre>

## (2)备注:
- 要测试的值，根据Shell模式的列表依次测试，发现匹配的时候，便执行相应的程序代码，直至;;为止.
- 可以使用多个模式使用|加以分割.
- 最后的*模式作为一个默认情况，可以省略.# 一 for循环:
## (1)功能:
- for循环:用于重复整个对象列表，依次执行每一个独立对象的循环内容.对象可以是命令行参数、文件名或是任何可以以列表格式建立的东西.

## (2)语法:
<pre><code>
省略in list则循环遍历整个命令行参数.
for name [ in list ]
do
...
done
例如:
打印出当前目录下的所有文件.反单引号``，表示执行中间的命令，引用结果为字符串.
for file in `ls .`
do
echo $file
done
</code></pre>


# 三 while循环和until循环:
## (1)语法:
<pre><code>
while condition
do
statements
done

until condition
do
statements
done

#condition可以是简单的命令列表，或者是包含&&与||的命令.
</code></pre>


## (2)while和until的区别:
- 只要condition是成功退出，while会继续循环；只要condition未成功结束，until则执行循环.

## (3)特例:无条件循环
<pre><code>
while true
do
...
done
</code></pre>



# 四 break和continue:
## (1)功能:
- break:跳出循环.break+n:跳出n层循环.
- continue:重新执行循环.continue+n:继续n层循环.
