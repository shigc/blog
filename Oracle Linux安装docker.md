---
title: Oracel Linux上安装docker
tags: [linux,docker]
categories: docker
date: 2021-4-20 10:22:31
---

### Oracel Linux上安装docker

#### 1. 安装必须的基本工具

`yum install -y yum-utils`

#### 2. 添加docker镜像repo

```
yum-config-manager \
    --add-repo \
    https://download.docker.com/linux/centos/docker-ce.repo
```

#### 3. 更新yum缓存

`yum makecache fast`

#### 4. 安装docker

`yum install docker-ce docker-ce-cli containerd.io`

#### 5. 运行docker守护进程

`systemctl start docker`


FAQ:

1. 安装docker时提示Requires: fuse-overlayfs >= 0.7和Requires: slirp4netns >= 0.4的解决方法

   添加下面内容到/etc/yum.repos.d/docker-ce.repo最前面，然后执行`yum -y install slirp4netns fuse-overlayfs container-selinux`

   ```
   [centos-extras]
   name=Centos extras - $basearch
   baseurl=http://mirror.centos.org/centos/7/extras/x86_64
   enabled=1
   gpgcheck=0
   ```

