# RSA_NestingDoll

## 题目信息
- 赛事：CISCN 2025 初赛
- 分类：Crypto

## 考点
- 嵌套 RSA 模数
- Pollard p-1 分解外层
- 内层因子与 φ(n) 恢复明文

## 解题思路
1. 外层大整数 N 可用 Pollard p-1（指数爬升 + gcd）拆成多个因子。
2. 每个外层因子减一再与内层 n 求 gcd，得到内层素数，算 φ 与 d 解密。

## 关键代码/payload
原文未给出可摘录的短代码，请参阅参考链接中的完整 exploit。

## 参考链接
- https://godownio.github.io/2025/12/20/2025-ciscn-chu-sai-wp-by-yp0int/

> 本文为对公开 writeup 的归纳总结，版权归原作者所有；请务必阅读原文核对细节。
