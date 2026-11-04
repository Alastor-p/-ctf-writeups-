---
title: crypto02
competition: 网鼎杯
year: 2024
category: Crypto
tags: [朱雀, rsa, coppersmith, high-bits]
sources:
  - https://sechub.in/view/2965877
  - https://www.ctfiot.com/217506.html
  - https://github.com/CTF-Archives/2024-wdb-zhuque
---

# crypto02

## 题目信息

- 赛事：第四届网鼎杯 2024 线上资格赛 · 朱雀组
- 分类：Crypto
- 题面：赛中补过提示。给出 1024 位量级的 `n`、`e = 0x10001`、`flag.enc`，以及 `p` 的高 256 bit。题单见 [CTF-Archives](https://github.com/CTF-Archives/2024-wdb-zhuque)。

## 考点

- 已知素因子高位的 Coppersmith / `small_roots`
- 已知位数不够时先爆破低位再跑格

## 解题思路

高半部分只有 256 bit，直接对整段未知位做 Coppersmith 出不来。公开 WP 先在本地测参数：`epsilon ≈ 0.014` 时大约能吃掉 248 bit 未知量。于是只爆破高位后面的约 8 bit，再对 `f = (p>>248)<<248 + x` 求 `small_roots`（`beta` 约 0.49）。恢复 `p` 后算 `d`，解密 `flag.enc`。

ChaMd5 的笔记按 1024 位 `n`、爆破量和 `epsilon` 的对应关系来估时间；Van1sh 的镜像按 512 位素数、高 256 bit 来写。两边位数表述不一样，以附件里 `n` 的比特长度为准。

## 关键代码/payload

```text
R.<x> = Zmod(n)[]
f = (p_high << unknown_bits) + x
f.small_roots(X=2^unknown_bits, beta=0.49, epsilon=0.014)
```

## 参考链接

- https://sechub.in/view/2965877
- https://www.ctfiot.com/217506.html
- https://github.com/CTF-Archives/2024-wdb-zhuque

> 本文为对公开 writeup 的归纳总结，版权归原作者所有；请务必阅读原文核对细节。
