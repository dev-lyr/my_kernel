# 一 概述:
## (1)功能:
- SystemTap从**运行**中的linux系统收集信息, 用来协助性能诊断和功能问题排查.
- SystemTap eliminates the need for the developer to go through the tedious and disruptive instrument, recompile, install, and reboot sequence that may be otherwise required to collect data.

## (2)使用:
- SystemTap provides a simple command line interface(**stap命令**) and scripting language for writing instrumentation for a live running kernel plus user-space applications.
- Among other tracing/probing tools, SystemTap is the tool of choice for complex tasks that may require live analysis, programmable on-line response, and whole-system symbolic access. 
- SystemTap can also handle simple tracing jobs.

## (3)相关技术:
- kprobe: Documentation/kprobes.txt.
- dtrace
- ebpf

## (4)SystemTap部署:
- 部署SystemTap, 以root身份安装两个rpm包: yum install systemtap systemtap-runtime.
- 使用SystemTap还需安装系统kernel对应的kernel-devel-{uname -r}.rpm, kernel-debuginfo-{uname -r}.rpm和kernel-debuginfo-common-{uname -r}.rpm包, 可使用stap-prep来安装依赖包, 若失败需手动安装.
- 安装后测试: stap -v -e 'probe vfs.read {printf("read performed\n"); exit()}'

## (5)备注:
- http://sourceware.org/systemtap/
- http://debuginfo.centos.org/
- https://sourceware.org/systemtap/SystemTap_Beginners_Guide/

# 二 stap命令:
## (1)功能:
- systemtap脚本翻译器(translator)/驱动器(driver), 是systemtap的前端工具.
- 可通过命名文件指定指令脚本(FILENAME), 或标准输入代替FILENAME, 或从命令行(使用-e SCRIPT).
- 该程序终止方式: 被用户中断; 脚本调用exit函数; 足够多的soft错误.

## (2)原理:
- 接收用指定语言写的probing指令, 将这些指令翻译为C代码, 编译C代码, 并且load最后的module到运行中的linux kernel来执行需要的系统trace/probe函数.

## (3)常用选项:
- -p NUM: 在NUM步骤后停止, 可选值1-5: parse, elaborate, translate, compile和run.
