---
title: 程序的编译和链接
tags: [c,programming]
categories: programming
---


### 1. 程序的编译
编译过程分为两个阶段：编译和汇编，而源文件的编译过程又包含两个主要阶段：编译预处理和编译
> 预编译：编译预处理读取源代码，对其中的伪指令和特殊符号进行处理。宏展开、引用文件展开等动作均在这个过程完成。
```
//first.c
#include <stdio.h>
#include "api.h"

#define SYS_NAME "linux"

int main(int argc, char **argv)
{
    printf("hello world! %s\n", SYS_NAME);
    print_hello();
}
```

预编译将.c文件转换成.i文件，使用的gcc命令时gcc -E，通过gcc -E first.c -o first.i 生成预编译文件，可以看到源码中引用的头文件中对应定义被”内联“宏展开

```
......
extern char *ctermid (char *__s) __attribute__ ((__nothrow__ , __leaf__));
# 840 "/usr/include/stdio.h" 3 4
extern void flockfile (FILE *__stream) __attribute__ ((__nothrow__ , __leaf__));

extern int ftrylockfile (FILE *__stream) __attribute__ ((__nothrow__ , __leaf__)) ;

extern void funlockfile (FILE *__stream) __attribute__ ((__nothrow__ , __leaf__));
# 868 "/usr/include/stdio.h" 3 4

# 2 "first.c" 2
# 1 "api.h" 1

# 1 "api.h"
void print_hello();
# 3 "first.c" 2

int main(int argc, char **argv)
{
    printf("hello world! %s\n", "linux");
    print_hello();
}
```

> 编译：编译程序索要做的工作就是通过词法分析和语法分析，在确认所有的指令都符合语法规则之后，将其翻译成等价的中间代码来表示或汇编代码

编译将.c/.h文件转换成.s文件，使用的gcc命令是gcc -S，通过gcc -S first.i -o first.s命令将预编译文件生成汇编代码

```
        .file   "first.c"
        .text
        .section        .rodata
.LC0:
        .string "linux"
.LC1:
        .string "hello world! %s\n"
        .text
        .globl  main
        .type   main, @function
main:
.LFB0:
        .cfi_startproc
        pushq   %rbp
        .cfi_def_cfa_offset 16
        .cfi_offset 6, -16
        movq    %rsp, %rbp
        .cfi_def_cfa_register 6
        subq    $16, %rsp
        movl    %edi, -4(%rbp)
        movq    %rsi, -16(%rbp)
        leaq    .LC0(%rip), %rsi
        leaq    .LC1(%rip), %rdi
        movl    $0, %eax
        call    printf@PLT
        movl    $0, %eax
        call    print_hello@PLT
        movl    $0, %eax
        leave
        .cfi_def_cfa 7, 8
        ret
        .cfi_endproc
.LFE0:
        .size   main, .-main
        .ident  "GCC: (Ubuntu 7.5.0-3ubuntu1~18.04) 7.5.0"
        .section        .note.GNU-stack,"",@progbits
```

> 汇编：汇编过程实际上是指把汇编语言代码翻译成目标机器指令的过程。对于被翻译系统处理的每一个源代码，都将最终进过这一处理而得到相应的目标文件，目标文件是为二进制文件，通常为.o文件。

汇编将.s文件转换成.o文件，使用的gcc命令时gcc -c，编译命令是as。通过as first.s -o first.o命令把汇编代码生成机器语言代码，使用objdump -t first.o 命令查看生成的符号表。

```
first.o：     文件格式 elf64-x86-64

SYMBOL TABLE:
0000000000000000 l    df *ABS*  0000000000000000 first.c
0000000000000000 l    d  .text  0000000000000000 .text
0000000000000000 l    d  .data  0000000000000000 .data
0000000000000000 l    d  .bss   0000000000000000 .bss
0000000000000000 l    d  .rodata        0000000000000000 .rodata
0000000000000000 l    d  .note.GNU-stack        0000000000000000 .note.GNU-stack
0000000000000000 l    d  .eh_frame      0000000000000000 .eh_frame
0000000000000000 l    d  .comment       0000000000000000 .comment
0000000000000000 g     F .text  0000000000000038 main
0000000000000000         *UND*  0000000000000000 _GLOBAL_OFFSET_TABLE_
0000000000000000         *UND*  0000000000000000 printf
0000000000000000         *UND*  0000000000000000 print_hello
```

### 2. 程序的链接
汇编程序生成的目标文件并不能直接执行，其中可能还有许多没有解决的问题。例如，某个源文件中的函数可能引用了另外一个源文件中定义的某个符号；在程序中可能调用了某个库函数等等。所有这些问题都需要经过链接程序处理才得以解决


* 程序的链接是将多个.o文件相应的段进行合并，建立映射关系并且合并符号表，进行符号解析，符号解析完成后就是给符号分配的虚拟地址。
* 将分配好的虚拟地址与符号表中定义的符号一一对应起来，使其成为正确的地址，使代码段的指令可以根据符号的地址执行相应的操作，最后由链接器生成可执行文件。

链接处理可以分为静态链接和动态链接。linux下静态链接生成是.a文件，动态链接生成是.so文件。

静态链接方式生成程序
```
gcc -c api.c -o api.o
ar rcs -o api.a api.o
gcc -static -g -o first_s first.c api.a
```





