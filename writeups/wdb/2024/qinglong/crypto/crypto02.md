---
title: crypto02
competition: 网鼎杯
year: 2024
category: Crypto
tags: [青龙, ecdsa, nonce-reuse, aes, vigenere]
sources:
  - https://mp.weixin.qq.com/s/HhL4lqcL_3EeYg1TDeBOKg
  - https://www.ctfiot.com/215151.html
  - https://cn-sec.com/archives/3331560.html
  - https://www.cnblogs.com/backlion/p/18527653
---

# crypto02

## 题目信息

- 赛事：第四届网鼎杯 2024 线上资格赛 · 青龙组
- 分类：Crypto
- 题面：flag 先做古典密码，再用 AES-CBC 包一层。AES 密钥来自一条 secp256k1 上的 ECDSA 私钥。

## 考点

- ECDSA 临时私钥 `k` 重用
- AES-CBC（密钥为 `SHA256(dA)`）
- 已知密钥的维吉尼亚

## 解题思路

公开源码里，flag 先用密钥 `WANGDINGCUP` 做字母移位（维吉尼亚）。同一 `k` 对两条消息签名，`r` 相同，`s1,s2,z1,z2` 都打印出来。由

`s = (z + r·dA) · k^{-1} mod n`

消掉 `k` 就能恢复 `dA`。`SHA256(dA)` 当 AES-CBC 密钥，密文前 16 字节是 IV。解出来的字母再按密钥做反向移位，并转成小写，得到 flag。不同转载里的具体 `r,s,z` 和密文十六进制并不相同，按自己的附件代入即可。

## 关键代码/payload

```text
k = (z1 - z2) * inv(s1 - s2) mod n
dA = (s1 * k - z1) * inv(r) mod n
AES_key = SHA256(dA)   # 再按 WANGDINGCUP 做减法移位
```

## 参考链接

- https://mp.weixin.qq.com/s/HhL4lqcL_3EeYg1TDeBOKg
- https://www.ctfiot.com/215151.html
- https://cn-sec.com/archives/3331560.html
- https://www.cnblogs.com/backlion/p/18527653

> 本文为对公开 writeup 的归纳总结，版权归原作者所有；请务必阅读原文核对细节。
