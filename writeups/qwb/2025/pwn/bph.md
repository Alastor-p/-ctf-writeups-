---
title: "Bph"
competition: "强网杯"
year: 2025
category: "Pwn"
tags:
  - "超大 size 使 malloc 失败后的任意偏移写 null"
  - "未初始化栈泄露 libc"
  - "劫持 stdout 做 FSOP / ORW"
sources:
  - "https://cn-sec.com/archives/4597169.html"
  - "https://blog.wm-team.cn/index.php/archives/87/"
---
# Bph

## 题目信息
- 赛事：强网杯 2025 初赛
- 分类：Pwn

## 考点
- 超大 size 使 malloc 失败后的任意偏移写 null
- 未初始化栈泄露 libc
- 劫持 stdout 做 FSOP / ORW

## 解题思路
1. token 输入可从栈上泄露 libc 相关指针。
2. `add` 在巨大 size 失败路径上仍能按 size 做偏移写 null（类似 R3CTF 某题手法）。
3. 控制 stdin/stdout FILE 结构完成任意写，再 ORW 读 flag。

## 关键代码/payload
原文未给出可摘录的短代码，请参阅参考链接中的完整 exploit。

## 参考链接
- https://cn-sec.com/archives/4597169.html
- https://blog.wm-team.cn/index.php/archives/87/

> 本文为对公开 writeup 的归纳总结，版权归原作者所有；请务必阅读原文核对细节。
