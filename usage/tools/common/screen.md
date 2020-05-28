# 一 概述:
## (1)常用:
- screen -S yourname -> 新建一个叫yourname的session
- screen -ls -> 列出当前所有的session
- screen -r yourname -> 回到yourname这个session
- screen -d yourname -> 远程detach某个session
- screen -d -r yourname -> 结束当前session并回到yourname这个session
- screen -x yourname：和他人共享一个会话。
- screen -t new_window_name：打开一个新的window，并重命名。

## (2)在每个screen下命令以(ctrl+a)开始, 例如：ctrl+a+d:
- C-a ? -> 显示所有键绑定信息
- C-a c -> 创建一个新的运行shell的窗口并切换到该窗口
- C-a n -> Next，切换到下一个 window
- C-a p -> Previous，切换到前一个 window
- C-a 0..9 -> 切换到第 0..9 个 window
- Ctrl+a [Space] -> 由视窗0循序切换到视窗9
- C-a C-a -> 在两个最近使用的 window 间切换
- C-a x -> 锁住当前的 window，需用用户密码解锁
- C-a d -> detach，暂时离开当前session，将目前的 screen session (可能含有多个 windows) 丢到后台执行，并会回到还没进 screen 时的状态，此时在 screen session 里，每个 window 内运行的 process (无论是前台/后台)都在继续执行，即使 logout 也不影响。
- C-a z -> 把当前session放到后台执行，用 shell 的 fg 命令则可回去。
- C-a w -> 显示所有窗口列表
- C-a t -> Time，显示当前时间，和系统的 load
- C-a k -> kill window，强行关闭当前的 window，或者quit也可关闭。
- C-a [ -> 进入 copy mode，在 copy mode 下可以回滚、搜索、复制就像用使用 vi 一样

## (3)配置文件：
- /etc/screenrc.