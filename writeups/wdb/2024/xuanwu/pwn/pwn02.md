---
title: pwn02
competition: 网鼎杯
year: 2024
category: Pwn
tags: [玄武, vfork, canary, ret2syscall]
sources:
  - https://www.ctfiot.com/214152.html
  - https://sechub.in/view/2966475
  - https://www.ctfiot.com/217930.html
  - https://cn-sec.com/archives/3460733.html
  - https://www.ctfiot.com/228428.html
---

# pwn02

## 题目信息

- 赛事：第四届网鼎杯 2024 线上资格赛 · 玄武组
- 分类：Pwn
- 题面：无符号表。启动时打印 `gift:`，内容是 canary。

## 考点

- `vfork` 父子共用栈，子进程的读能改父进程还没检查的局部变量
- 反编译看不出的分支：`[rbp-0x28] == 1` 进入后门，`[rbp-0x11c] == 0x11111111` 跳出循环
- 第一次读改掉第二次 `read` 的长度，再 `ret2syscall`

## 解题思路

`main` 里先 `vfork`。子进程先跑，父进程要等它结束。子进程那次 `read` 只有 `0x40` 字节，本身溢不出返回地址，但和父进程的栈是同一块，可以在返回父进程之前把 `[rbp-0x28]` 写成 `1`。父进程因此不走 “It's impossible”，而是返回到后面的循环。

循环里再次 `vfork`。子进程 `read` 名义上是 `0x100`，长度参数躺在这次输入能盖到的位置，所以第一次输入把长度改大，第二次才能溢出。canary 末字节常常是 `0`，后面的 `strcpy` 会截断，公开分析改用 `read` 溢出来铺 ROP，并用 `0x11111111` 让父进程退出循环、走到返回地址。gift 就是 canary，填回去之后 `execve("/bin/sh")`。

各文的 gadget 和「先改哪一格」顺序不完全相同，以自己 IDA 里的栈槽为准。完整 ROP 不收录。

## 关键代码/payload

```text
gift = canary
vfork 共享栈：把 [rbp-0x28] 写成 1，进入后门循环
子进程第一次输入改大 read 长度，并写入 0x11111111 跳出循环
第二次 read：canary + ret2syscall
```

## 参考链接

- https://www.ctfiot.com/214152.html
- https://sechub.in/view/2966475
- https://www.ctfiot.com/217930.html
- https://cn-sec.com/archives/3460733.html
- https://www.ctfiot.com/228428.html

> 本文为对公开 writeup 的归纳总结，版权归原作者所有；请务必阅读原文核对细节。
