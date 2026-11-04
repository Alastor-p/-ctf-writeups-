---
title: "ECDSA"
competition: "全国大学生信息安全竞赛"
year: 2025
category: "Crypto"
tags:
  - "NIST521p"
  - "私钥 = SHA512(固定欢迎语) mod n"
  - "nonce 也可由 `sha512(b\"bias\"+i)` 预测"
sources:
  - "https://godownio.github.io/2025/12/20/2025-ciscn-chu-sai-wp-by-yp0int/"
  - "https://moyuin.top/blog/%E9%95%BF%E5%9F%8E%E6%9D%AF%20WriteUP"
---
# ECDSA

## 题目信息
- 赛事：CISCN 2025 初赛
- 分类：Crypto

## 考点
- NIST521p
- 私钥 = SHA512(固定欢迎语) mod n
- nonce 也可由 `sha512(b"bias"+i)` 预测

## 解题思路
1. 阅读出题脚本可知私钥直接由 `SHA512(b"Welcome to this challenge!")` 对曲线阶取模得到。
2. 无需 lattice：本地重算 d，再按题目要求对 d 做 md5 等变换提交。

## 关键代码/payload
```python
d = int.from_bytes(sha512(b"Welcome to this challenge!").digest(),"big") % NIST521p.order
```

## 参考链接
- https://godownio.github.io/2025/12/20/2025-ciscn-chu-sai-wp-by-yp0int/
- https://moyuin.top/blog/%E9%95%BF%E5%9F%8E%E6%9D%AF%20WriteUP

> 本文为对公开 writeup 的归纳总结，版权归原作者所有；请务必阅读原文核对细节。
