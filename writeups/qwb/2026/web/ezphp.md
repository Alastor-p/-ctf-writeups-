---
title: ezphp
competition: 强网杯
year: 2026
category: Web
tags: [ssrf, gopher, redis, php-deserialize, pop-chain]
sources: [https://cn-sec.com/archives/5548848.html]
---

# ezphp

## 题目信息

- 分类：Web
- 题面：ezphp，how 2shell???（容器启动约 1 分钟）
- 公开解出：约 760 队

## 考点

- 源码泄漏 → 受限 SSRF（仅环回）
- gopher 打无认证 Redis 改 PHP Session
- Session 反序列化 + 依赖 POP 链写 WebShell

## 解题思路

公开 WP 利用链：源码泄漏摸清 SSRF 参数与协议黑名单 → 黑名单遗漏 gopher，经 SSRF 向本机 Redis 写 Session → 触发 `session_start()` 反序列化 → 依赖中的文件写 POP 链写入可访问 WebShell → 命令执行读目标文件。环回限制反而把火力集中到同机 Redis/应用。

## 关键代码/payload

```text
SSRF(gopher) → Redis SET PHPREDIS_SESSION:... → 反序列化 POP → webshell
```

（完整 RESP/payload 见源文，此处不展开。）

## 参考链接

- https://cn-sec.com/archives/5548848.html
