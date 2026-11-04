---
title: NeuronShuffle
competition: 强网杯
year: 2026
category: Misc
tags: ['numpy', 'rng', 'permutation', 'ml-weights']
sources: ['https://eryuemu.com/blog/qwb-2026-neuron-shuffle-license-recap/', 'https://cn-sec.com/archives/5548779.html']
---

# NeuronShuffle


## 题目信息

- 分类：Misc
- 附件：`check.py`、`model_A.npz`、`model_B.bin`
- 公开解出：约 630 队
- 公开复验 flag 形态：`flag{` + `sha256(canon)[:32]` + `}`

## 考点

- `np.random.default_rng` 种子复原
- 高斯尺度 σ 与拒绝采样“摇匀”
- 答案与模型结构解耦（次日种子 permutation）

## 解题思路

`model_A` 实为 `default_rng(20261101)`、`normal(0, 0.6)` 生成的伪权重（层宽约 32→48→40→32→16，含复制神经元与空类“沉淀”）。关键坑是默认 σ=1 的精确匹配会失败，需尺度无关比值检验扫出种子 20261101 并完整重放生成器。答案却不在标签序列化里，而是 `default_rng(20261102)` 对 48/40/32 的三个 `permutation`，用 `;` / `,` 连接后交给 `check.py` 哈希校验。`model_B.bin` 公开分析为高熵噪声干扰项。

## 关键代码/payload

```python
import numpy as np
rng = np.random.default_rng(20261102)
ps = [rng.permutation(n) for n in (48, 40, 32)]
canon = ";".join(",".join(map(str, p)) for p in ps)
# python3 check.py "$canon"
```

## 参考链接

- https://eryuemu.com/blog/qwb-2026-neuron-shuffle-license-recap/
- https://cn-sec.com/archives/5548779.html
