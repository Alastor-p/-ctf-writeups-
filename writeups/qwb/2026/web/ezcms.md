---
title: ezcms
competition: 强网杯
year: 2026
category: Web
tags: ['cms', 'sqli', 'file-upload', 'rce']
sources: ['https://cn-sec.com/archives/5548848.html']
---

# ezcms


## 题目信息

- 分类：Web
- 公开解出：约 467 队

## 考点

- CMS 审计（PostgreSQL `ILIKE` / 转义问题等）
- 后台媒体/上传至 RCE

## 解题思路

公开 WP：从 SQL 报错与 `ILIKE` 转义切入注入或鉴权绕过，进入 `/admin/media` 一类管理功能，再落到 easycms 用户权限下的命令执行（示例输出 `uid=1001(easycms)`），最终读 flag。

## 关键代码/payload

短摘录（报错形态，来自公开 WP）：

```text
SQLSTATE 42601 ... WHERE title ILIKE E'%''%' ORDER BY id DESC
```

## 参考链接

- https://cn-sec.com/archives/5548848.html
