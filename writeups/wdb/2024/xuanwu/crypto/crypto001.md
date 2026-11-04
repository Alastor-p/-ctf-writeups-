---
title: crypto001
competition: 网鼎杯
year: 2024
category: Crypto
tags: [玄武, shamir, linear-algebra]
sources:
  - https://www.ctfiot.com/217506.html
---

# crypto001

## 题目信息

- 赛事：第四届网鼎杯 2024 线上资格赛 · 玄武组
- 分类：Crypto
- 题面：去掉 `wdflag{}` 之后的字节被放进一个改过的 Shamir 分享。模数 257，玩家数等于 flag 长度 `n`，阈值是 `2n`。一共 10000 份 `.sobj`。

## 考点

- 分享值是「flag 字节 + 噪声」对已知系数的线性组合
- 噪声系数矩阵不满秩时，用左零空间把噪声消掉

## 解题思路

每份分享有 `n` 行、每行 `2n` 个系数。前 `n` 列对应 flag 字节，后 `n` 列对应随机噪声。系数和分享值都在文件里。

若噪声那一块 `C2` 不满秩，它的左核向量 `k` 满足 `k·C2 = 0`。同一 `k` 乘到分享值上，噪声被消掉，只留下关于 flag 的方程 `k·C1·flag = k·V`。公开 WP 扫完 10000 份，有 32 份满足秩的条件，而 flag 长度也是 32，把这些方程叠起来解一次线性方程，再按字节转成字符串（外面还要自己套回 `wdflag{}`）。

## 关键代码/payload

```text
C1 = coefs[:32]; C2 = coefs[32:]
若 rank(C2) < 32：k 取自 C2 的左核
k*C1*flag = k*values   （模 257）
```

## 参考链接

- https://www.ctfiot.com/217506.html

> 本文为对公开 writeup 的归纳总结，版权归原作者所有；请务必阅读原文核对细节。
