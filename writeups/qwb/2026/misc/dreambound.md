---
title: Dreambound
competition: 强网杯
year: 2026
category: Misc
tags: ['ml', 'rl', 'coordinate-descent', 'tcp-json']
sources: ['https://cn-sec.com/archives/5548779.html', 'https://github.com/CTF-Archives/2026-qwbs10-quals']
---

# Dreambound


## 题目信息

- 分类：Misc / AI
- 附件：`model.py`、`checkpoint.pt`、`requirements.txt`
- 公开解出：约 429 队
- 题面：Try to dream hallucinate。

## 考点

- 白盒策略/想象网络打分
- 离散动作序列搜索（坐标下降 + 扰动）
- 裸 TCP 一行 JSON 协议（非 HTTP）

## 解题思路

服务不是 HTTP，而是裸 TCP 上提交一行 JSON 动作序列并返回分数。公开 WP 逆向打分函数后排除简单均值/折扣假设，形式化为最大化模型“想象”分数；梯度法在离散动作上无效，改用批量评估 + 坐标下降 + 随机扰动跳出局部最优，得到超过阈值的动作序列后提交拿 flag。序列对模型分布外行为敏感，需在服务端复验。

## 关键代码/payload

（公开 WP 给出最优动作序列与坐标下降框架；此处略去完整序列，请对照源文复现。）

## 参考链接

- https://cn-sec.com/archives/5548779.html
