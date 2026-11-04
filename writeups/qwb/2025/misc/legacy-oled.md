---
title: "legacyOLED"
competition: "强网杯"
year: 2025
category: "Misc"
tags:
  - "PulseView 解 I2C"
  - "还原 OLED 显示帧"
  - "某一帧 PNG 的 LSB 隐写"
sources:
  - "https://cn-sec.com/archives/4592147.html"
---
# legacyOLED

## 题目信息
- 赛事：强网杯 2025 初赛
- 分类：Misc

## 考点
- PulseView 解 I2C
- 还原 OLED 显示帧
- 某一帧 PNG 的 LSB 隐写

## 解题思路
1. 用 PulseView 打开逻辑分析数据，I2C 解码后提取屏幕刷新数据并还原画面。
2. 在还原出的某一帧（如 frame_1040.png）做 LSB 隐写提取得到 flag。

## 关键代码/payload
原文未给出可摘录的短代码，请参阅参考链接中的完整 exploit。

## 参考链接
- https://cn-sec.com/archives/4592147.html

> 本文为对公开 writeup 的归纳总结，版权归原作者所有；请务必阅读原文核对细节。
