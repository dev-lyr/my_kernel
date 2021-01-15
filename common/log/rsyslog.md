# 一 概述:
## (1)功能:
- **Rsyslog** is a rocket-fast system for log processing. 
- It offers high-performance, great security features and a modular design.

## (2)备注:
- 对接kafka: https://www.rsyslog.com/doc/master/configuration/modules/omkafka.html

# 二 配置:
## (1)概述:
- Rsyslogd配置文件为rsyslog.conf, 通常在/etc目录下, 默认rsyslogd读取/etc/rsyslog.conf配置文件, 可通过命令行选项配置.
- 配置格式: basic(用来配置基本配置), advanced(配置其它非basic), obsolete legacy(遗留格式, 不建议使用).
