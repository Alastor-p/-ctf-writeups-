---
title: crypto01
competition: 网鼎杯
year: 2024
category: Crypto
tags: [白虎, gf2, linear-cipher, known-plaintext]
sources:
  - https://www.ctfiot.com/215151.html
  - https://mp.weixin.qq.com/s/5Xet54leUqVOeMYzTX0ROw
  - https://sechub.in/view/2964737
  - https://cn-sec.com/archives/3590373.html
---

# crypto01

## 题目信息

- 赛事：第四届网鼎杯 2024 线上资格赛 · 白虎组
- 分类：Crypto
- 题面：64 位块、14 轮。每轮是比特置换 `P`、线性变换 `S`、再异或密钥，最后 `P` 的逆。输出全部密文块和置换表。密钥是 `MD5(flag)` 的低 64 位。

## 考点

- 把置换和 `S` 写成 `GF(2)` 上的矩阵
- 中间轮的 `P` 与 `P^{-1}` 抵消
- 已知前缀爆破 1 字节恢复密钥

## 解题思路

`S` 是固定的移位异或再或上掩码，在 `GF(2)` 上是 `Ax+b`。公开分析把一轮收成 `T = P^{-1} A P`、`U = P^{-1} b`，14 轮后明文和密钥都落在线性方程里：

`c = T^{14} m + (T^{13}+…+I) U + (T^{13}+…+I) P^{-1} k`

flag 以 `wdflag{` 开头，最后一块再爆破一个字节当已知明文，就能解出候选 `k`，再解密全部块，用 `MD5(flag)` 低 64 位对上的那个就是答案。Van1sh 的镜像用 z3 对消掉中间 `P` 的方程求解，ChaMd5 直接在 Sage 里做矩阵，两条路是同一件事。

## 关键代码/payload

```text
T = Pinv * A * P
U = Pinv * b
c - T^14 * m - sum(T^i)*U = sum(T^i) * Pinv * k
```

## 参考链接

- https://www.ctfiot.com/215151.html
- https://mp.weixin.qq.com/s/5Xet54leUqVOeMYzTX0ROw
- https://sechub.in/view/2964737
- https://cn-sec.com/archives/3590373.html

> 本文为对公开 writeup 的归纳总结，版权归原作者所有；请务必阅读原文核对细节。
