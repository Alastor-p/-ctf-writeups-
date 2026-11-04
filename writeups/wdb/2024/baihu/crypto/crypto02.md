---
title: crypto02
competition: 网鼎杯
year: 2024
category: Crypto
tags: [白虎, rsa, common-prime, pollard-rho]
sources:
  - https://www.ctfiot.com/215151.html
  - https://mp.weixin.qq.com/s/5Xet54leUqVOeMYzTX0ROw
  - https://sechub.in/view/2964737
  - https://jayxv.github.io/2019/11/11/%E5%AF%86%E7%A0%81%E5%AD%A6%E5%AD%A6%E4%B9%A0%E7%AC%94%E8%AE%B0%E4%B9%8B%E6%B5%85%E6%9E%90Pollard's%20rho%20algorithm%E5%8F%8A%E5%85%B6%E5%BA%94%E7%94%A8/
---

# crypto02

## 题目信息

- 赛事：第四届网鼎杯 2024 线上资格赛 · 白虎组
- 分类：Crypto
- 题面：`p = 2·g·a+1`，`q = 2·g·b+1`，`g` 约 1000 bit，`a`、`b` 各约 24 bit 量级的素数，`e = 65537`。附件是 `N` 和密文。

## 考点

- Common Prime RSA
- Pollard's rho，迭代函数取成 `x ↦ x^{n-1}+3 (mod n)` 一类

## 解题思路

`p-1` 与 `q-1` 共享大因子 `g`。公开 WP 直接套 2019 年同一结构的 Pollard's rho 笔记：用 `gcd(x1-x2, n)` 拆出 `p`，再算 `d` 解密。Van1sh 注明当年常用的 map 是 `x^{n-1}+3`，并提到后来的笔记里有收敛更好的 map。完整迭代和本题的 `n` 见原文，不在这里重复。

## 关键代码/payload

```text
p = 2*g*a + 1
q = 2*g*b + 1
# Pollard rho: map x -> (x^(n-1) + 3) mod n
```

## 参考链接

- https://www.ctfiot.com/215151.html
- https://sechub.in/view/2964737
- https://jayxv.github.io/2019/11/11/%E5%AF%86%E7%A0%81%E5%AD%A6%E5%AD%A6%E4%B9%A0%E7%AC%94%E8%AE%B0%E4%B9%8B%E6%B5%85%E6%9E%90Pollard's%20rho%20algorithm%E5%8F%8A%E5%85%B6%E5%BA%94%E7%94%A8/

> 本文为对公开 writeup 的归纳总结，版权归原作者所有；请务必阅读原文核对细节。
