---
title: reverse01
competition: 网鼎杯
year: 2024
category: Reverse
tags: [白虎, apk, aes, junk-code]
sources:
  - https://mp.weixin.qq.com/s/5Xet54leUqVOeMYzTX0ROw
  - https://sechub.in/view/2964737
  - https://github.com/CTF-Archives/2024-wdb-baihu
---

# reverse01

## 题目信息

- 赛事：第四届网鼎杯 2024 线上资格赛 · 白虎组
- 分类：Reverse
- 题面：Android so。`JNI_OnLoad` 不能直接 F5。题单见 [CTF-Archives](https://github.com/CTF-Archives/2024-wdb-baihu)。

## 考点

- 间接跳转花指令（`BR` 实际落到下一条）
- `init_array` 里替换真正的 native
- 魔改 AES：自定义 S-box，并且 `MixColumns` 与 `ShiftRows` 对调

## 解题思路

公开 WP 先把落在下一条指令上的 `BR X8` 以及同类间接跳转 NOP 掉，so 才能反编译。真正的检查不在表面的 `JNI_OnLoad`：`init_array` hook 了 `RegisterNatives`，实现落在 `sub_1A9A8`。

该函数是 tiny-AES 风格的 CBC，但 S-box 整表被换掉，加密轮里 `MixColumns` 跑在 `ShiftRows` 前面。密钥和 IV 在文中都是 `01..10` 这 16 个递增字节，密文 48 字节。把魔改后的逆运算套回 CBC 即可。S-box 全表在原文，这里不复制。

## 关键代码/payload

```text
NOP 掉 BR 花指令
真函数 sub_1A9A8：自定义 S-box，MixColumns 与 ShiftRows 互换
AES-CBC decrypt，key = IV = 01 02 ... 10
```

## 参考链接

- https://mp.weixin.qq.com/s/5Xet54leUqVOeMYzTX0ROw
- https://sechub.in/view/2964737

> 本文为对公开 writeup 的归纳总结，版权归原作者所有；请务必阅读原文核对细节。
