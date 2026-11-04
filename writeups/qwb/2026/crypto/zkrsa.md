---
title: zkRSA
competition: 强网杯
year: 2026
category: Crypto
tags: [gq-identification, rsa, ec-prng, protocol-bug]
sources: [https://cn-sec.com/archives/5548779.html, https://github.com/CTF-Archives/2026-qwbs10-quals]
---

# zkRSA

## 题目信息

- 分类：Crypto
- 题面：Let me tell you a story about zkRSA.
- 公开解出：约 210 队

## 考点

- Guillou–Quisquater 身份证明变体与错误验证方程
- 定义在 Z_n 上的椭圆曲线横坐标 PRNG（16 路平移）
- 协议层伪造应答绕过（无需真正求根）

## 解题思路

公开 WP：服务端本意是 GQ 证明，但 V 误把私钥 x 当作校验指数，且在读 `com` 前打印 `y`。若猜中挑战 `chal=c`，令 `com = y^(-c) mod n`、`res=1`，则等式恒成立。挑战来自 `ECGenerator`：曲线在 Z_n 上，下一步横坐标仅有 16 种候选（由隐藏纵坐标 `mod 16` 选平移点）。对 16 候选各构造一轮伪造即可通过验证并拿 flag。题眼是协议实现错误，而非经典 ZK 安全性。

## 关键代码/payload

```text
# 对每个候选 chal=c：
#   com = inv(y^c) mod n, res = 1
```

## 参考链接

- https://cn-sec.com/archives/5548779.html
- https://github.com/CTF-Archives/2026-qwbs10-quals
