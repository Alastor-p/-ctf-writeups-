---
title: hoRRibleRing
competition: 强网杯
year: 2026
category: Crypto
tags: [rlwe, decision-lwe, lattice]
sources: [https://cn-sec.com/archives/5548779.html, https://github.com/xiaoshabi-cmd/qiangwangbei2026, https://github.com/CTF-Archives/2026-qwbs10-quals]
---

# hoRRibleRing

## 题目信息

- 分类：Crypto
- 题面：Notice that there are 3 “R”s in the title too :(
- 公开解出：约 606 队

## 考点

- Ring-LWE 判定样本逐 bit 编码 flag
- 区分 `(a, a·s+e)` 与均匀对
- 多项式环参数与统计/格手段

## 解题思路

公开合集：flag 每位对应一条样本——bit0 为真正 Ring-LWE（离散高斯 s,e，σ≈3.37，模约 512 次多项式），bit1 为均匀随机 `(a,b)`；大端 bit 序拼字节。攻击目标是对每条样本做判定。星宇Sec 文给出可解路线；xiaoshabi 仓库另归档了部分降维/格路线的负面结论，复现时以合集题解为主并避开已证伪分支。

## 关键代码/payload

```python
# bit=0: b = (a*s + e) % f
# bit=1: a,b uniform
# output 顺序 = flag 大端比特串
```

## 参考链接

- https://cn-sec.com/archives/5548779.html
- https://github.com/xiaoshabi-cmd/qiangwangbei2026
