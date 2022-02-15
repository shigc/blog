---
title: 汇编语言程序设计 - 环境搭建
tags: [assembly]
categories: assembly
---
使用visual studio 2010和masm32搭建win32汇编语言开发环境

### 安装masm32：
1. 从官网 [http://www.masm32.com](http://www.masm32.com) 下载最新的安装包
2. 以管理员权限运行安装程序

### 安装AsmHighlighter：
下载地址https://download.csdn.net/download/barrysgy/10718561

#### 使用visual studio 2010创建项目：
1. 新建一个空白项目

2. 选中项目-右键-生成自定义-选择masm

![image-20220212163511877](D:/develop/Blog/images/image-20220212163511877.png)

3. 项目属性-配置属性-链接器-系统-子系统修改为控制台 (/SUBSYSTEM:CONSOLE)

4. 项目属性-配置属性-Microsoft Macro Assembler-General-Include Paths添加masm32的include目录

5. 项目属性-配置属性-链接器-常规-附加附加库目录添加masm32的lib目录

6. 新建一个hello.asm文件

```
.486
.model flat, stdcall
option casemap :none   ; case sensitive

include windows.inc
include masm32.inc
include kernel32.inc
include macros.asm

includelib masm32.lib
includelib kernel32.lib

.code
start:
    print "Hello world"
    exit
end start
```

7. 生成解决方案

**Tips:**

上面步骤如果没有出现Microsoft Macro Assembler配置，请先添加一个.asm后缀结尾的文件到项目

