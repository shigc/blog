---
title: ubuntu server服务器环境搭建
tags: [linux,ubuntu]
categories: linux
date: 2023-7-23 10:22:31
---

### ubuntu server服务器环境搭建

#### 1.docker环境

##### 1.1 安装docker

* 更新系统软件

  ```
  sudo apt update
  sudo apt upgrade
  sudo apt install wget apt-transport-https gnupg2 software-properties-common
  ```

* 导入gpg密钥和docker源

  ```
  # 导入docker源
  echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list
  
  # 更新gpp密钥
  curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
  ```

* 安装docker

  ```
  sudo apt update
  sudo apt install docker-ce docker-ce-cli containerd.io docker-compose-plugin
  ```

* 验证安装

  ```
  docker -v
  ```

* 启动docker

  ```
  sudo systemctl enable docker
  sudo systemctl start docker
  sudo systemctl status docker
  ```

##### 1.2 安装portainer

* 创建portainer数据卷

  ```
  #创建卷
  docker volume create portainer_data
  
  #查看卷
  docker volume inspect portainer_data
  ```

* 安装portainer

  ```
  docker run -d -p 9000:9000 --name=portainer --restart=always -v /var/run/docker.sock:/var/run/docker.sock -v portainer_data:/data portainer/portainer-ce:latest
  ```

##### 1.3 安装hassio

```
# 安装homeassistant
docker run -d --name homeassistant -p 8123:8123 --privileged --restart=unless-stopped -e TZ=Asia/Shanghai \
-v /mnt/file/config/hassio:/config --network=host homeassistant/qemux86-64-homeassistant:latest

# 安装hassio
docker run -d --name=hassio_supervisor \
        --env=SUPERVISOR_NAME=hassio_supervisor \
        --env=SUPERVISOR_MACHINE=qemux86-64 \
        --env=SUPERVISOR_SHARE=/mnt/file/config/hassio \
        --volume=/mnt/file/config/hassio:/data:rw \
        --volume=/run/docker.sock:/run/docker.sock:rw \
        --volume=/run/dbus:/run/dbus:ro \
        --volume=/run/udev:/run/udev:ro \
        --volume=/etc/machine-id:/etc/machine-id:ro \
        --privileged \
        --workdir=/ \
        --restart=no \
        --runtime=runc \
        hassiocn/amd64-hassio-supervisor:latest
```





