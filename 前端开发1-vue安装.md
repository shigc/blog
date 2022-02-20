---
title: vue环境搭建
tags: [vue,web]
categories: vue
date: 2021-11-20 10:18:40
---

## 1. vue环境搭建

### 1.1 安装node.js

[Node.js下载地址](https://nodejs.org/en/download/)，选择对应平台下载安装，使用默认设置安装即可

### 1.2 设置node.js全局和缓存路径（可选）

1. 在nodejs安装路径下，新建node_global和node_cache两个文件夹

2. 设置缓存文件夹

   ```
   npm config set cache "<nodejs安装路径>\node_cache"
   ```

3. 设置全局模块存放路径

   ```
   # 设置成功后，之后用命令npm install XXX -g安装以后模块会放在设置的node_global目录里面
   npm config set prefix "<nodejs安装路径>\node_global"
   ```

### 1.3 安装cnpm(淘宝镜像) 

```
npm install -g cnpm --registry=https://registry.npm.taobao.org
```

### 1.4 设置环境变量

添加NODE_PATH环境变量，值为<nodejs安装路径>\node_global\node_modules

并添加<nodejs安装路径>\node_global到PATH中

### 1.5 安装vue

```
cnpm install vue -g
```

### 1.6 安装vue-cli 脚手架

```
cnpm install vue-cli -g
```

### 1.7 全局安装webpack

```
cnpm install webpack -g
```

