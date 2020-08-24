---
title: SSH客户端连接服务器超时问题
tags:
  - ssh
  - 超时
categories: Linux
excerpt: 'SSH客户端连接服务器超时，主要修改两个配置项的值，ClientAliveInterval,ClientAliveCountMax'
abbrlink: f30f991e
date: 2020-08-24 15:38:49
---
## 问题描述
用SSH客户端连接linux服务器时，经常会出现与服务器会话连接中断现象，造成这个问题的原因是SSH服务有自己独特的会话连接机制。

## 解决方案
### 1、设置服务器向SSH客户端连接会话发送频率和时间
```sh
vi /etc/ssh/sshd_config
ClientAliveInterval 60 //定义了每隔多少秒给SSH客户端发送一次信号
ClientAliveCountMax 86400 //定义了超过多少秒后断开与ssh客户端连接
```
### 2、重新启动系统SSH服务
```
service sshd restart
```
大功告成！
