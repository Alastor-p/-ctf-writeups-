---
title: GraphNexus
competition: 羊城杯
year: 2026
category: Web
tags: ['websocket', 'h2', 'sqli', 'create-alias', 'rce']
sources: ['https://xz.aliyun.com/news/93039']
---

# GraphNexus

## 题目信息

- 分类：WEB（Ktor + WebSocket 协作）
- 入口：平台代理公网地址（详情里的私有 IP 隧道不可用）
- 帧：魔数 `NXUS` + opcode + BE len + payload

## 考点

- 空 SUBSCRIBE 可获会话；QUERY DSL 的 `SQL()` 直通 H2
- 解析器丢弃末尾 `)` → 在括号前加空格保留引号构造任意 SQL
- H2 `CREATE ALIAS` + Runtime.exec；`/readflag` setuid

## 解题思路

1. WebSocket 握手 → SUBSCRIBE → QUERY。
2. `SQL(… )` 执行任意语句；`CREATE ALIAS` 定义 shell 包装后 `CALL`。
3. 执行 `/readflag` 取 flag。

## 关键代码/payload

```text
SQL(CREATE ALIAS IF NOT EXISTS EXEC AS '…Runtime.exec…' )
SQL(CALL EXEC('/readflag') )
```

## 参考链接

- https://xz.aliyun.com/news/93039
