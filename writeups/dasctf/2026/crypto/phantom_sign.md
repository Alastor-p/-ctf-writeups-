---
title: phantom_sign
competition: DASCTF夏季赛
year: 2026
category: Crypto
tags: ['ecdsa', 'biased-nonce', 'hnp', 'lll']
sources:
  - 'https://j-0k3r.github.io/2026/06/01/2026DASCTF夏季赛/'
  - 'https://q1uju.cc/posts/dasctf2026summer_writeup/'
---

# phantom_sign

## 题目信息

- 分类：Crypto
- secp256k1 ECDSA；40 条签名；`k_i = urandom(31)` → `k < 2^248`（相对 256-bit 阶偏 8 bit）
- Flag：`DASCTF{3cd5a_b1as3d_n0nc3_HNP_l4tt1c3_4ttack!}`

## 考点

- Biased nonce → Hidden Number Problem；Kannan 嵌入 / 构造格 + LLL 恢复 `d`
- AES key = `sha256(long_to_bytes(d))[:16]`

## 解题思路

1. 由 `k ≡ h s^{-1} + d r s^{-1} (mod n)` 建 HNP 实例。
2. 格基归约得短向量中的 `d`；校验所有 `k_i < 2^248`。
3. 解密密文得 flag。

## 关键代码/payload

```text
# Sage/flint LLL on Kannan-embedded lattice (dim ~ 41)
# 完整矩阵构造见原文；此处不展开长脚本
```

## 参考链接

- https://j-0k3r.github.io/2026/06/01/2026DASCTF夏季赛/
- https://q1uju.cc/posts/dasctf2026summer_writeup/
