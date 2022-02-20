---
title: 安卓手机用作电脑的HTTP代理服务器
tags: [android,proxy]
categories: Android
date: 2021-7-20 10:27:14
---
目前电脑上的免费VPN软件比较难找，但是安卓上的免费VPN软件很多，所以考虑手机翻墙后作为电脑端的HTTP代理服务器，让电脑端也可以科学上网

### 手机端设置：

1. 下载安装Termux，google play上可以直接下载

2. 在Termux上安装Python
``` bash
$ apt install python
```
3. 安装[HTTP代理服务器](https://github.com/abhinavsingh/proxy.py "proxy.py")脚本
``` bash
$ pip install proxy.py
```
4. 运行HTTP代理服务器（默认端口是8899，可以用port参数指定端口）
``` bash
$ proxy.py --hostname  <手机局域网IP地址>
```
<strong> 备注：
1. hostname参数不配置的话，默认使用的IP是127.0.0.1，这时手机只能作为本机的代理服务器
2. 手机和电脑必须在同一个局域网下（保证手机和电脑能建立连接） </strong>

### 电脑端设置：
1. 设置IE的代理:Internet选项--连接--局域网设置--代理服务器，地址为手机局域网地址，端口8899，你也可以安装一些快速切换代理的插件来设置，这里就不多说明了

#### Tips:
手机通过电脑代理上网也可以类似地进行操作，在电脑上安装Python和proxy.py，然后运行proxy.py

#### 参考文章：
[知乎：用Android手机做电脑的HTTP代理服务器](https://zhuanlan.zhihu.com/p/22683468)