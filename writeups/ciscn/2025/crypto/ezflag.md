---
title: "EzFlag"
competition: "全国大学生信息安全竞赛"
year: 2025
category: "Crypto"
tags:
  - "口令门后按斐波那契索引查表生成 flag"
  - "模 16 的 Pisano 周期为 24，可优化"
sources:
  - "https://l0serqianxia.github.io/blog/2025/12/29/ciscn-2025-personal-writeup/"
  - "https://moyuin.top/blog/%E9%95%BF%E5%9F%8E%E6%9D%AF%20WriteUP"
  - "https://godownio.github.io/2025/12/20/2025-ciscn-chu-sai-wp-by-yp0int/"
---
# EzFlag

## 题目信息
- 赛事：CISCN 2025 初赛
- 分类：Crypto

## 考点
- 口令门后按斐波那契索引查表生成 flag
- 模 16 的 Pisano 周期为 24，可优化

## 解题思路
1. 输入正确口令 `V3ryStr0ngp@ssw0rd` 后进入生成循环；直接跑会因 `f(a1)` 循环次数指数增大而极慢。
2. `f` 本质是斐波那契第 n 项模 16，周期 24，故用 `n % 24` 模拟。
3. 查表 `K = "012ab9c3478d56ef"`，并在固定位置插 `-`，得到 flag。

## 关键代码/payload
```python
K="012ab9c3478d56ef"
def f(n):
    n%=24; a,b=0,1
    for _ in range(n): a,b=b,(a+b)&0xF
    return K[a]
```

## 参考链接
- https://l0serqianxia.github.io/blog/2025/12/29/ciscn-2025-personal-writeup/
- https://moyuin.top/blog/%E9%95%BF%E5%9F%8E%E6%9D%AF%20WriteUP
- https://godownio.github.io/2025/12/20/2025-ciscn-chu-sai-wp-by-yp0int/

> 本文为对公开 writeup 的归纳总结，版权归原作者所有；请务必阅读原文核对细节。
