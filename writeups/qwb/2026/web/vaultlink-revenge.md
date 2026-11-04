---
title: vaultlink_revenge
competition: 强网杯
year: 2026
category: Web
tags: ['metadata', 'hardening', 'ssrf']
sources: ['https://cn-sec.com/archives/5548848.html']
---

# vaultlink_revenge


## 题目信息

- 分类：Web（vaultlink 加强版）
- 公开解出：约 150 队

## 考点

- 在原题链路上的额外加固绕过
- 仍可能涉及内部服务与元数据

## 解题思路

公开 Web9：在 vaultlink 基础上关闭或限制了部分捷径，需按合集步骤组合新的信息泄漏与信任链才能读到 `/flag`。请对照源文与原题差异点复现。

## 关键代码/payload

见 https://cn-sec.com/archives/5548848.html Web9。

## 参考链接

- https://cn-sec.com/archives/5548848.html
