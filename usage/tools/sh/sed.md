- 一 概述：
- 
- (1)功能：
- 
- 流编辑器，用来对输入流进行基本的文本转换.

- (2)常用选项:
- 
- -f script-file
- -i：直接修改输入文件.
- -n：显示匹配的行.

- 二 常用：
- 
- (1)查询指定行：
- 
- sed -n Np file：显示第N行。
- sed -n 'M，Np' file：显示文件的M-N行。
- sed -n 'M，$p' file：显示第M行到最后。
- sed -n '/pattern/p' file：显示匹配pattern的行。

- (2)删除删除指定行(同查询)：
- 
- sed 'Md' file：删除file的第M行。
- sed 'M,Nd' file：删除第M到N行。
- sed '/^$/d' file：删除空白行。

- (3)替换：
- 
- sed 's/被替换的字符串/新的字符串/[替换选项]'
- sed 's/M/N/' file：只替换每行的第一个。
- sed 's/M/N/g' file：全部替换。
- sed sed 's/M/N/' file默认会显示所有行，若想只显示替换行，则sed -n 's/M/N/p' file.