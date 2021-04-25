# 一 概述:
## (1)概述:
- SystemTap脚本是SystemTap会话的基础, 脚本控制SystemTap收集上面类型的消息以及收集到消息后怎么处理.
- SystemTap脚本由两块组成: **events**和**handlers**, SystemTap session运行中, SystemTap monitor系统的指定事件, 并在事件发生时执行对应handler.
- **Probe**: 一个event和它对应handler的集合, systemtap脚本可以包含多个probe.
- SystemTap脚本以.stp命令.

## (2)SystemTap脚本类型:
- Probe scripts: identify probe points and associated handlers.
- Tapset scripts:  /usr/share/systemtap/tapset/, 预定义的一些probe和函数库, 可在SystemTap脚本中使用, 不能直接运行.

## (3)语法:
- probe的格式: probe event {语句}, 支持单个probe多个event, 事件以逗号分开, 当任一一个事件发生时handler都会执行.
- function的格式: function 函数名(参数){语句}, 主要是为了避免重复语句.
- 备注: https://sourceware.org/systemtap/langref/

## (4)events类型:
- 同步事件: syscall.system_call, vsf.file_operation, kernel_function("function")等.
- 异步事件: begin, end, timer events.

## (5)handlers
- probe的handler通常也称作probe body, 即{}内的语句.

## (6)备注:
- https://sourceware.org/systemtap/langref/
