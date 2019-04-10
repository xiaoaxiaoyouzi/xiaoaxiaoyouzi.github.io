---
layout:   post
title:    Crypto RSA
subtitle:   Hello world,hello blog!
date:     2019-04-10
author:   吴柚
header-img: post-bg-desk.jpg
catalog:    true
tags:
    - 学习
---

## 题目分析

![](https://i.loli.net/2019/04/09/5caca91327cda.png)

查看题目，可以看到题目所给两个文件，一个是包含flag的加密文件，另一个从文件名来看是私钥，所以此题应该是采用非对称加密。由于直接给出了私钥和使用公钥加密的文件，因此考虑直接使用工具openssl来进行解题。

## openssl介绍

1. 基本介绍：OpenSSL 是一个安全套接字层密码库，囊括主要的密码算法、常用的密钥和证书封装管理功能及SSL协议，并提供丰富的应用程序供测试或其它目的使用。

2. 基本功能：openssl是一个开源程序的套件、这个套件有三个部分组成：一是libcryto，这是一个具有通用功能的加密库，里面实现了众多的加密库；二是libssl，这个是实现ssl机制的，它是用于实现TLS/SSL的功能；三是openssl，是个多功能命令行工具，它可以实现加密解密，甚至还可以当CA来用，可以让你创建证书、吊销证书。

## 解题过程

1. 在Linux虚拟机中安装openssl最新版本以及一些必要的库；

2. 打开终端，输入命令`openssl`进入openssl；

3. 使用指令，用私钥对flag.encrypt进行解密，输出为flag.txt

```
rsautl -decrypt -inkey rsa_private_key.pem -in flag.encrypt -out flag.txt

```

4. 打开flag.txt，即可得到解题的flag。flag为flag{you_maY_Kn0w_AbouT_RSA}。

![](https://i.loli.net/2019/04/09/5cacab577ad52.png)
