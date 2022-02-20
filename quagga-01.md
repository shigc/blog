---
title: quagga的安装和使用
tags: [quagga,router]
categories: Quagga
date: 2021-3-20 10:22:10
---
Quagga软件原名是Zebra是由一个日本开发团队编写的一个以GNU版权方式发布的软件

### 1.下载源码并编译安装：
```
[root@centos code]# git clone https://gitee.com/opensi/quagga.git
[root@centos code]# cd quagga/
[root@centos code]# ./configure --enable-tcp-zebra --enable-mpls --enable-ldpd --enable-vtysh --enable-user=root --enable-group=root --enable-vty-group=root
[root@centos quagga]# make && make install
```
<!--[root@centos quagga]# ./configure --enable-vtysh --enable-user=root --enable-group=root --enable-vty-group=root-->


### 2.复制配置文件到quagga默认配置目录下
```
[root@centos quagga]# cp zebra/zebra.conf.sample /usr/local/etc/
[root@centos quagga]# cp ospfd/ospfd.conf.sample /usr/local/etc/
[root@centos quagga]# cp ldpd/ldpd.conf.sample /usr/local/etc/
```
### 3.启动相关进程
```
[root@centos quagga]# zebra -d
[root@centos quagga]# ospfd -d
[root@centos quagga]# ldpd -d
```

tips:
1、如果vmware无法ping通windows，但是windows可以ping通vware虚拟机，需要关闭windows防火墙
2、如果zebra收到报文但是ospf无法建立，需要关闭系统防火墙

#### 参考文章：
[Linux上实现mpls，ldpd（Quagga）完整步骤](https://blog.csdn.net/simonczw/article/details/52538671)