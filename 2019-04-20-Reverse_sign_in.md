---
layout:   post
title:    Reverse sign in
subtitle:   Hello world,hello blog!
date:     2019-04-20
author:   吴柚
header-img: post-bg-desk.jpg
catalog:    true
tags:
    - 学习
---

今天继续reverse中的Reverse Sign In。

![](https://i.loli.net/2019/02/25/5c74093d8ed08.png)

先使用斯托夫文件格式分析器分析出该文件为ELF文件

![](https://i.loli.net/2019/02/25/5c740a0b1dc49.png)

然后使用IDA打开该文件，直接定位到主函数部分

![](https://i.loli.net/2019/02/25/5c74094004eef.png)

按F5键进入伪代码部分，并分析出有一个sub_400686函数决定了Flag的对错，所以对这个函数进行分析

![](https://i.loli.net/2019/02/25/5c740942754cc.png)

![](https://i.loli.net/2019/04/20/5cbb20910830e.png)

该函数的主体为if语句，主要含义为：如果形参a1中每个字符异或byte_400818[i]中的字符 不等于i成立 则 return 0。所以要想 return 1，则 (char)(*(_BYTE *)(i + a1) ^ byte_400818[i]) == i

然后再查看byte_400818[i]里的数据，可以按快捷键H将16进制转化为10进制。

![](https://i.loli.net/2019/04/20/5cbb20905cac3.png)

看到这里发现不懂dup啥意思，所以去google了一下，在这里作为一个补充。

dup指令：Dup用于把一个相同值赋值若干次。

```
重复次数 dup（数据项）
具体比如：s db 30 dup（0）
定义一个字节型变量，该变量占用30个字节，所有字节被初始化成0
```

所以上述数据中的，`2 dup(96)` 含义为`96,96`。

由此，我们得到了byte_400818[i]中全部的数据，现在可以写脚本得到flag。

```
# -*- coding:utf-8 -*-
n =  [102, 109, 99, 100, 127, 60, 54, 114, 87, 66, 100, 59,123, 82, 124, 60, 102, 84, 96, 96, 39, 74, 73, 127,113, 88, 82, 114, 125, 117, 42, 98, 0]

for i in range(0,32):
    print(chr(n[i] ^ i))
```

得到flag:`flag{90u_Kn0w_r3vErs3__hiAHiah4}`

![](https://i.loli.net/2019/04/20/5cbb2406155ec.png)

查资料后知道还有一种验证flag是否正确的方法，即使用gdb打开该文件，然后输入flag。

![](https://i.loli.net/2019/04/20/5cbb275c305e5.png)

使用`gdb r`指令后，我先尝试输入flag，结果right，然后尝试输入其他指令，则结果wrong，由此，该flag正确。
