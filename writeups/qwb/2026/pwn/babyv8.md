---
title: Babyv8
competition: 强网杯
year: 2026
category: Pwn
tags: ['v8', 'sandbox', 'maglev']
sources: ['https://blog.h-acker.cn/5688.html', 'https://github.com/CTF-Archives/2026-qwbs10-quals']
---

# Babyv8


## 题目信息

- 分类：PWN
- 公开题解合集收录于星宇Sec / 阻击者联盟转载
- 附件/环境：见 https://github.com/CTF-Archives/2026-qwbs10-quals

## 考点

- v8, sandbox, maglev

## 解题思路

V8 sandbox： Maglev 补丁致 Smi/对象混淆，造 fake JSArray；劫持 FeedbackCell `cached_entrypoint` 调 `/readflag`。

（赛题 flag 多为动态容器值；公开 WP 中静态样例已脱敏。完整利用步骤与偏移表见源文对应章节。）

## 关键代码/payload

公开合集含较长 PoC。本仓库只保留思路摘要，**不复制完整 exploit**；请直接阅读：

- https://blog.h-acker.cn/5688.html

## 参考链接

- https://blog.h-acker.cn/5688.html
- https://github.com/CTF-Archives/2026-qwbs10-quals
