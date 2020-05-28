# 一 概述:
## (1)功能:
- Apache Http Server基准测试工具, 基于URL, 也可以测试nginx、jetty等.

## (2)用法:
- ab 选项 [http[s]://]hostname[:port]/path

## (3)常用选项:
<pre><code>
-c concurrency: 设置请求的并发度.
-n requests: 设置总的请求数量.
-t timelimit: 设置测试的总时间.
-s timeout: 等待socket超时的时间, 默认为30s.
-i : 用HEAD替代GET.
-m HTTP-method: 自定义HTTP方法.
-k: 开启Http keepalive.
-p post-file: POST的文件.
-T content-type: POST或PUT方法的Content-type头部, 默认为text/plain.
-X proxy[:port]: 使用代理服务器.
-H custom-header: 添加额外的头部到请求中.
-A auth-username:password: 支持基本的用户验证.
-P proxy-auth-username:password: 支持途中代理的基本用户验证.
</code></pre>