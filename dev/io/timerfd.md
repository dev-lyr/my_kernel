# 一 概述:
## (1)概述
- These system calls create and operate on a timer that delivers timer expiration notifications via a file descriptor. 
- They provide an alternative to the use of setitimer(2) or timer_create(2), with the advantage that the file descriptor may be monitored by select(2), poll(2), and epoll(7).

## (2)API:
- timerfd_create
- timerfd_settime
- timerfd_gettime
