---
title: "adventure"
competition: "强网杯"
year: 2025
category: "Pwn"
tags:
  - "商店购买数量整数溢出"
  - "屠龙后戒指 `use` 中 `strcpy` 覆盖描述指针"
  - "泄露 + 任意写 → House of Apple / 伪造 `_IO_list_all`"
sources:
  - "https://cn-sec.com/archives/4597169.html"
---
# adventure

## 题目信息
- 赛事：强网杯 2025 初赛
- 分类：Pwn

## 考点
- 商店购买数量整数溢出
- 屠龙后戒指 `use` 中 `strcpy` 覆盖描述指针
- 泄露 + 任意写 → House of Apple / 伪造 `_IO_list_all`

## 解题思路
1. 商店对数量检查不严，大正数溢出后可零成本购炸弹屠龙。
2. 屠龙戒指 `use` 存在 `strcpy`，可覆盖 ring 描述相关指针；反复买卖戒指放大原语。
3. 先泄地址，再控制描述指针任意写，结合超长 C++ string 申请大 chunk 伪造 IO_FILE，打 House of Apple。

## 关键代码/payload
原文未给出可摘录的短代码，请参阅参考链接中的完整 exploit。

## 参考链接
- https://cn-sec.com/archives/4597169.html

> 本文为对公开 writeup 的归纳总结，版权归原作者所有；请务必阅读原文核对细节。
