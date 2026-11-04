---
title: cwp
competition: 强网杯
year: 2026
category: Web
tags: ['php', 'sql-injection', 'ssrf', 'command-injection']
sources: ['https://cn-sec.com/archives/5548848.html', 'https://github.com/CTF-Archives/2026-qwbs10-quals']
---

# cwp


## 题目信息

- 分类：Web
- 目标：`/root/flag.txt`
- 附件：blog 源码包
- 公开解出：约 1340 队

## 考点

- PHP 博客执行器/钩子数组错位
- SQL 注入与快照 hook 重放
- 内网服务再攻击与命令注入

## 解题思路

公开合集 Web2：从源码审计入手，利用执行器数组或 hook 注册错位扩大攻击面，串起 SQL 注入 → 快照/hook 重放 → 访问内网组件 → 命令注入读 flag。多层信任边界错误是题眼。

## 关键代码/payload

（多阶段利用链较长，仅保留思路；请求样例见 https://cn-sec.com/archives/5548848.html。）

## 参考链接

- https://cn-sec.com/archives/5548848.html
