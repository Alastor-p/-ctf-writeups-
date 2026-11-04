---
title: crypto01
competition: 网鼎杯
year: 2024
category: Crypto
tags: [青龙, rsa, boneh-durfee, partial-key]
sources:
  - https://mp.weixin.qq.com/s/HhL4lqcL_3EeYg1TDeBOKg
  - https://www.ctfiot.com/215151.html
  - https://cn-sec.com/archives/3331560.html
  - https://www.cnblogs.com/naby/p/18514581
  - https://sechub.in/view/2962999
---

# crypto01

## 题目信息

- 赛事：第四届网鼎杯 2024 线上资格赛 · 青龙组
- 分类：Crypto
- 题面：512 位素数 `p`、`q`，`d` 是 299 位素数，`e = d^{-1} mod φ(n)`。输出 `n,e,c`，以及 `p`、`q` 各 70 个高位。

## 考点

- 小私钥 RSA（Boneh–Durfee / Herrmann–May）
- 已知素因子高位，用来收紧格攻击里的 `y` 界

## 解题思路

公开脚本把 `δ = 299/1024 < 1-√2/2`，所以现成的 Boneh–Durfee 模板可以直接套。高位已经给出，不必再爆破 MSB：用 `hint` 拼出 `p0`、`q0`，把方程写成 `1 + x(A+y)`，对模 `e` 做格规约求 `d`，再解密 `c`。多篇 WP 都指向同一类高校赛 / CryptoCTF 原题模板，参数只换成本场的 `n,e` 和 70 bit hint。

## 关键代码/payload

```text
d = getPrime(299)
e = inverse(d, (p-1)*(q-1))
hint1 = p >> (512-70)
# pol = 1 + x*(A+y) 模 e，delta = 299/1024
```

## 参考链接

- https://mp.weixin.qq.com/s/HhL4lqcL_3EeYg1TDeBOKg
- https://www.ctfiot.com/215151.html
- https://cn-sec.com/archives/3331560.html
- https://www.cnblogs.com/naby/p/18514581
- https://sechub.in/view/2962999

> 本文为对公开 writeup 的归纳总结，版权归原作者所有；请务必阅读原文核对细节。
