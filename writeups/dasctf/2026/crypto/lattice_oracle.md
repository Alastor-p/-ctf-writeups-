---
title: lattice_oracle
competition: DASCTF夏季赛
year: 2026
category: Crypto
tags: ['lwe', 'brute-force', 'aes']
sources:
  - 'https://j-0k3r.github.io/2026/06/01/2026DASCTF夏季赛/'
  - 'https://q1uju.cc/posts/dasctf2026summer_writeup/'
---

# lattice_oracle

## 题目信息

- 分类：Crypto（LWE 玩具参数）
- `n=6, q=97, m=30`；`s[i]∈{0,1,2,3}`；`e∈{-1,0,1}`
- AES-CBC 密钥：`sha256(str(s))[:16]`
- Flag：`DASCTF{LWE_l4tt1c3_r3duct10n_i5_p0w3rful!}`

## 考点

- 参数过小：秘密空间 `4^6=4096` 可穷举，无需 LLL

## 解题思路

1. 枚举全部 `s`，检查每条样本误差是否落在 `{-1,0,1}`（注意模 `q` 折返）。
2. 派生 AES key，CBC 解密去 padding。
3. 公开脚本给出 `s=[0,0,2,1,1,1]`（以可复现脚本为准）。

## 关键代码/payload

```python
from itertools import product
for s in product(range(4), repeat=6):
    # e_i = (b_i - <A_i,s>) mod q ∈ {-1,0,1}
    ...
```

## 参考链接

- https://j-0k3r.github.io/2026/06/01/2026DASCTF夏季赛/
- https://q1uju.cc/posts/dasctf2026summer_writeup/
