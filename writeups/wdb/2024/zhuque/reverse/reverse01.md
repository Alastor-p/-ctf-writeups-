---
title: reverse01
competition: 网鼎杯
year: 2024
category: Reverse
tags: [朱雀, smc, base24]
sources:
  - https://sechub.in/view/2965877
  - https://github.com/CTF-Archives/2024-wdb-zhuque
---

# reverse01

## 题目信息

- 赛事：第四届网鼎杯 2024 线上资格赛 · 朱雀组
- 分类：Reverse
- 题面：需要先补自修改，才能看到后面的编码。见 [CTF-Archives](https://github.com/CTF-Archives/2024-wdb-zhuque)。

## 考点

- SMC：一段代码每个字节加 `0x42`
- 自定义码表的 base24，结果还要倒序

## 解题思路

ChaMd5 用 IDAPython 从 `0x140003000` 起连续 `0x600` 字节做 `(b+0x42) & 0xff`。补完后是自定义 base24：码表 `4836CR7F9TXGQVWYB2JPHKDM`，密文按 24 进制聚成一个大整数再转字节，最后把字符串反转。密文和码表以原文为准。

## 关键代码/payload

```text
PatchByte(0x140003000+i, (Byte(...)+0x42) & 0xff)  # i in 0..0x600
base24 码表 "4836CR7F9TXGQVWYB2JPHKDM"
decode(cipher)[::-1]
```

## 参考链接

- https://sechub.in/view/2965877

> 本文为对公开 writeup 的归纳总结，版权归原作者所有；请务必阅读原文核对细节。
