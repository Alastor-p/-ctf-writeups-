# check-little

## 题目信息
- 赛事：强网杯 2025 初赛
- 分类：Crypto

## 考点
- RSA + AES 混合
- e=3
- `gcd(ciphertext, N)` 意外分解 N

## 解题思路
1. 题目给出 N、e=3、AES 的 iv 与密文等。
2. 先对 RSA 密文与 N 求 gcd，若明文与 N 不互素则可直接得到因子，再还原后续 AES 密钥与 flag。

## 关键代码/payload
```python
p = gcd(c, N)  # 若 p 非平凡则分解成功
```

## 参考链接
- https://cn-sec.com/archives/4597169.html

> 本文为对公开 writeup 的归纳总结，版权归原作者所有；请务必阅读原文核对细节。
