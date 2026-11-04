---
title: frozen
competition: 强网杯
year: 2026
category: Crypto
tags: ['falcon', 'ldl-tree', 'bit-flip', 'ntru']
sources: ['https://github.com/xiaoshabi-cmd/qiangwangbei2026', 'https://cn-sec.com/archives/5548779.html']
---

# frozen


## 题目信息

- 分类：Crypto
- 公开解出：约 874 队
- 目标：从被位翻转污染且截去头部 1024 个 double 的内存转储恢复 `D = f·adj(f)+g·adj(g)`，再解密 flag

## 考点

- Falcon / LDL 树内存布局
- FFT 与回文/`t` 反回文结构
- 腐蚀下的树修复与整数性判别

## 解题思路

公开 writeup：`expanded_doubles` 先写满 FFT(f/g/F/G) 共 1024 个 double（恰被砍掉），剩余为树节点与叶子。`_T(G00)` 子树编码 `FFT(D)`。利用 `L_j=t_j·ρ_j`、`t` 反回文与父节点线性反解，在 `t²` 域做一致性；quad 最小腐坏穷举 + 父级反解定叶子，再用 `D` 整数残差选唯一候选。NTRU 格攻击在公开分析中被排除（代价过高）。

## 关键代码/payload

短摘录：

```python
# 逆变换须用 M.T（公开 WP 强调的陷阱）
D = solve(M.T, E)
```

完整求解见源仓库 `solve_frozen.py`。

## 参考链接

- https://github.com/xiaoshabi-cmd/qiangwangbei2026/blob/main/frozen_02136a685ccd425e537aa0735795019f/writeup.md
- https://cn-sec.com/archives/5548779.html
