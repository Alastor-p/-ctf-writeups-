---
title: three_friends
competition: DASCTF夏季赛
year: 2026
category: Crypto
tags: ['rsa', 'common-factor', 'gcd']
sources:
  - 'https://j-0k3r.github.io/2026/06/01/2026DASCTF夏季赛/'
  - 'https://q1uju.cc/posts/dasctf2026summer_writeup/'
---

# three_friends

## 题目信息

- 分类：Crypto
- flag 切三段分别 RSA；`n1=p*q, n2=q*r, n3=p*r`，`e=65537`
- Flag：`DASCTF{thr33_fri3nds_sh@r3_pr1m3s!!}`

## 考点

- 三模数两两共享素因子 → `gcd` 直接分解

## 解题思路

1. `q=gcd(n1,n2)`，`p=n1//q`，`r=n2//q`（或等价两两 gcd）。
2. 分别算 `d_i`，解密三段拼接。

## 关键代码/payload

```python
from math import gcd
from Crypto.Util.number import long_to_bytes, inverse
q = gcd(n1, n2); p = n1 // q; r = n2 // q
# d1=inverse(e,(p-1)*(q-1)); ...; flag = m1||m2||m3
```

## 参考链接

- https://j-0k3r.github.io/2026/06/01/2026DASCTF夏季赛/
- https://q1uju.cc/posts/dasctf2026summer_writeup/
