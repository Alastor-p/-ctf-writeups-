---
title: VVMM
competition: 羊城杯
year: 2026
category: Reverse
tags: ['windows', 'custom-vm', 'arx', 'invert']
sources: ['https://xz.aliyun.com/news/93035', 'https://xz.aliyun.com/news/93039']
---

# VVMM

## 题目信息

- 分类：逆向（Windows PE，自研 VMC2）
- 输入长度 31；`--check` / `--run` 可验证
- Flag：`flag{J1nxI_i5_4_6eautiful_g1rl}`

## 考点

- 容器解密出字节码；ISA 细节：字节内存、ROLI 只转低 8 位、STAGE 为 murmur 风格 S-box、内存初值非零模式
- 1 段装载 + 7 轮就地 ARX；末尾 31 字节常量比较
- 每轮每字节对自身双射 → 从后往前枚举 0..255 求逆

## 解题思路

1. 解码有效程序记录，对照 handler 写对齐模拟器（用 `--run` 的 steps/pc/acc 差分校准）。
2. 自比较常量反向解 7 轮再解第 1 段，得到可打印 31 字节。
3. `--bof` 为干扰，不产生 flag。

## 关键代码/payload

```text
# 逐块: for v in 0..255: exec_block; match out[i]
# 正向 ACCEPT → flag{J1nxI_i5_4_6eautiful_g1rl}
```

## 参考链接

- https://xz.aliyun.com/news/93035
- https://xz.aliyun.com/news/93039
