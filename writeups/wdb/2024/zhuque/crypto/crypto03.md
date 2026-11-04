---
title: crypto03
competition: 网鼎杯
year: 2024
category: Crypto
tags: [朱雀, rsa, coppersmith, polynomial-gcd]
sources:
  - https://sechub.in/view/2965877
  - https://www.ctfiot.com/217506.html
  - https://github.com/CTF-Archives/2024-wdb-zhuque
---

# crypto03

## 题目信息

- 赛事：第四届网鼎杯 2024 线上资格赛 · 朱雀组
- 分类：Crypto
- 题面：三组辅助模数，外加 `m1 = p1·m² + p2·m + p3`、`m2 = q1·m² + q2·m + q3` 在另一对 RSA 下的密文。见 [CTF-Archives](https://github.com/CTF-Archives/2024-wdb-zhuque)。

## 考点

- 近似倍数的素数：`q1 = nextprime(2024·p1)`
- `n2` 与 `p2²+q2²` 联立
- 生成脚本写错素数判断后的高位泄漏
- 两个多项式的快速 GCD 求公共根 `m`

## 解题思路

第一层：`q1` 略大于 `2024·p1`，对 `n1/2024` 开方就落到 `p1` 附近。

第二层：已知 `n2 = p2·q2` 和 `n22 = p2²+q2²`，解这个二元二次即可。

第三层脚本里两处循环都写成 `while not is_prime(p3)`，`q3` 的素性实际上没被检查。公开测试是 `n3` 开方后高位（约 528 bit）和 `p3` 相同，再做一次已知高位攻击。

三组 `p,q` 都有了之后，未知数只剩 `m`。`c1`、`c2` 是 `f(m)`、`g(m)` 在最外层模数下的 `e` 次方，`f`、`g` 就是上面两个二次式。公开 WP 按明文相关攻击，对这两个多项式做 GCD 求公共根；直接 GCD 会爆递归，改用 `fast_polynomial_gcd`（2023 SEECTF 罗密欧与朱丽叶，crypto-attacks 里也有）。

## 关键代码/payload

```text
p1 ≈ isqrt(n1 // 2024); q1 = nextprime(2024*p1)
n22 = p2**2 + q2**2, n2 = p2*q2
# q3 的循环条件误写成 is_prime(p3)
# fast_gcd( f(x)^e - c1 , g(x)^e - c2 ) 模 n
```

## 参考链接

- https://sechub.in/view/2965877
- https://www.ctfiot.com/217506.html

> 本文为对公开 writeup 的归纳总结，版权归原作者所有；请务必阅读原文核对细节。
