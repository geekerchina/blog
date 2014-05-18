---
layout: post
title:  "IO Smashthestack level1"
date:   2014-05-18 22:30:01
categories: writeup
---

#Introduction
先看README.cn
打开/levels/
直接gdb level01
disassemble main
![level01_smash_the_stack](../public/img/level01_140518.png)

将0x10f转换为十进制是271

./level01
输入271即可