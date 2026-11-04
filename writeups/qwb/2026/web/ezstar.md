---
title: ezstar
competition: 强网杯
year: 2026
category: Web
tags: ['pwn-in-web', 'uaf', 'fsop']
sources: ['https://cn-sec.com/archives/5548848.html']
---

# ezstar


## 题目信息

- 分类：Web（实则偏二进制利用的 Web 服务）
- 题面：How to HackStar?
- 公开解出：约 279 队

## 考点

- 堆 UAF / 虚表伪造
- `setcontext` + ROP
- 无界写触发

## 解题思路

公开 WP 将利用概括为：释放再复用泄漏对象地址与 libc → 修补控制块与相邻 chunk 头 → 伪造虚表在析构时 `setcontext` → 控制块伪造成 `ucontext_t` 跳 ROP → `d_len=0` 触发无界写。属 Web 题面下的原生 pwn 链。

## 关键代码/payload

高阶步骤见源文；此处不附完整 exploit。

## 参考链接

- https://cn-sec.com/archives/5548848.html
