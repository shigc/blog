---
title:x64汇编语言程序设计 - 常用寄存器
tags: [assembly]
categories: assembly
date: 2024-6-2 20:36:53
---

## 常用寄存器

| QWORD（8字节） | DWORD（4字节） | WORD（2字节） | BYTES（1字节） | 说明         |
| -------------- | -------------- | ------------- | -------------- | ------------ |
| RAX            | EAX            | AX            | AH，AL         | 返回值       |
| RBX            | EBX            | BX            | BH，BL         | 被调用者保存 |
| RCX            | ECX            | CX            | CH，CL         | 第4个参数    |
| RDX            | EDX            | DX            | DH，DL         | 第3个参数    |
| RSI            | ESI            | SI            | SIL            | 第2个参数    |
| RDI            | EDI            | DI            | DIL            | 第1个参数    |
| R8             | R8D            | R8W           | R8B            | 第5个参数    |
| R9             | R9D            | R9W           | R9B            | 第6个参数    |
| R10            | R10D           | R10W          | R10B           | 调用者保存   |
| R11            | R11D           | R11W          | R11B           | 调用者保存   |
| R12            | R12D           | R12W          | R12B           | 被调用者保存 |
| R13            | R13D           | R13W          | R13B           | 被调用者保存 |
| R14            | R14D           | R14W          | R14B           | 被调用者保存 |
| R15            | R15D           | R15W          | R15B           | 被调用者保存 |
| RSP            | ESP            | SP            | SPL            | 栈指针       |
| RBP            | EBP            | BP            | BPL            | 被调用者保存 |

说明：对32位寄存器进行修改时，寄存器高32位将会被置为0，但是对16位寄存器或者8位寄存器进行修改操作不影响高位



