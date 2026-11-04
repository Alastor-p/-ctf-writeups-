---
title: vaultlink
competition: 强网杯
year: 2026
category: Web
tags: ['metadata', 'websocket', 'ssrf', 'cloud']
sources: ['https://cn-sec.com/archives/5548848.html', 'https://github.com/CTF-Archives/2026-qwbs10-quals']
---

# vaultlink


## 题目信息

- 分类：Web
- 场景：金融网关 + 内部 relay/core
- 目标：容器内 `/flag`
- 公开解出：约 1065 队

## 考点

- 未鉴权维护口泄漏 seed / relay
- WebSocket AUTH 边界
- 云元数据 / ECI user-data 读 Pod 配置

## 解题思路

公开 WP 三步：① 维护端口无鉴权读 seed 与 relay；② relay WebSocket `AUTH admin <seed>` 返回仅管理台可用，说明 flag 不在此；③ 打云元数据取 ECI user-data 中的 Pod spec 解码得到 flag 相关秘密。

## 关键代码/payload

思路级：

```text
1) 维护口 → seed, relay
2) AUTH admin <seed> → auth-console-only
3) 元数据 user-data → Pod spec → flag
```

## 参考链接

- https://cn-sec.com/archives/5548848.html
