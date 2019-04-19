---
layout:   post
title:    HelloWorld反汇编分析
subtitle:   Hello world,hello blog!
date:     2019-04-19
author:   吴柚
header-img: post-bg-desk.jpg
catalog:    true
tags:
    - 学习
---

## 学习目的

由于第三阶段的测试中需要对未知的指令集进行分析，，故今天简单尝试了对HelloWorld.c程序进行分析。

### 学习过程

HelloWorld程序源代码：

```
#include <stdio.h>
 
int main(int argc, char *argv[])
{
printf("Hello world!");
return 0;
}

```

下面是使用反汇编工具得到的汇编代码，，使用注释对程序进行分析。

```
push   rbp                        //保存栈低，上一帧函数信息
mov    rbp,rsp                    //保存栈顶
sub    rsp,0x20                   //栈顶下移动 32个字节，开辟栈空间
mov    DWORD PTR [rbp+0x10],ecx   //传入第一个参数，保存在 ebp + 16字节处
mov    QWORD PTR [rbp+0x18],rdx   //传入第二个参数，保存在ebp + 24字节处
call   0x4026b0 <__main>//进入main函数

lea    rcx,[rip+0x7b05]           // 0x409020 //传入字符串地址
call   0x4075d0 <printf>          // 调用printf函数

mov    eax,0x0
add    rsp,0x20                   //恢复堆栈
pop    rbp
ret   
```

经过今天的学习，发现对于数据在内存中的地址、运算并不算很熟练，故我需要继续对汇编语言进行学习，同时也要参考《深入理解计算机系统》。
