# 一 概述：
## (1)功能:
- 内核对AIO(Asynchronous IO)的支持, 通过系统调用(io_submit)提交一个或多个I/O请求无需等待完成, 通过单独的接口io_getevents来获取已完成的I/O操作.

## (2)场景:
- O_DIRECT方式打开的文件的AIO, 例如:ext2,ext3等, 不支持非O_DIRECT模式的打开的文件.
- raw或O_DIRECT设备上的AIO.
- 不支持socket和管道上的AIO.

## (3)备注:
- libaio可设置IO完成后的回调函数.
- libaio可和epoll结合使用.

# 二 源码:
## (1)概述:
- 头文件libaio.h

## (2)系统调用:
- extern int io_setup(int maxevents, io_context_t *ctxp);
- extern int io_destroy(io_context_t ctx);
- extern int io_submit(io_context_t ctx, long nr, struct iocb *ios[]);
- extern int io_cancel(io_context_t ctx, struct iocb *iocb, struct io_event *evt);
- extern int io_getevents(io_context_t ctx_id, long min_nr, long nr, struct io_event *events, struct timespec *timeout);