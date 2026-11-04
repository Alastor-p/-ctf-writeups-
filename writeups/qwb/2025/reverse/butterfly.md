---
title: "butterfly"
competition: "强网杯"
year: 2025
category: "Reverse"
tags:
  - "硬编码 8 字节密钥 `MMXEncod`"
  - "按 8 字节块：减密钥 → 循环右移 1 → 半字字节交换 → 再异或密钥"
sources:
  - "https://cn-sec.com/archives/4597169.html"
  - "https://blog.wm-team.cn/index.php/archives/87/"
---
# butterfly

## 题目信息
- 赛事：强网杯 2025 初赛
- 分类：Reverse

## 考点
- 硬编码 8 字节密钥 `MMXEncod`
- 按 8 字节块：减密钥 → 循环右移 1 → 半字字节交换 → 再异或密钥

## 解题思路
1. 密钥文件前 8 字节与程序硬编码一致，确认为 `MMXEncod`。
2. 对 `encode.dat` 每 8 字节逆变换即可得到明文 flag。

## 关键代码/payload
```c
uint64_t decrypt(uint64_t enc, uint64_t key) {
  // 逐字节减 key → 循环右移 1 → 每 16bit 高低字节互换 → XOR key
}
```

## 参考链接
- https://cn-sec.com/archives/4597169.html
- https://blog.wm-team.cn/index.php/archives/87/

> 本文为对公开 writeup 的归纳总结，版权归原作者所有；请务必阅读原文核对细节。
