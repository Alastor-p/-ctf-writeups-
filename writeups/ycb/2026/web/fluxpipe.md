---
title: FluxPipe
competition: 羊城杯
year: 2026
category: Web
tags: ['elixir', 'sqli', 'crc-oracle', 'erlang-cookie', 'fpx']
sources: ['https://xz.aliyun.com/news/93039']
---

# FluxPipe

## 题目信息

- 分类：WEB
- 栈：Elixir Plug/Cowboy + PostgreSQL；对外 HTTP:4000，内部 FPX:4001 未直接暴露
- 从发布包 BEAM/LitT 恢复隐藏路由

## 考点

- 管道搜索 `status` raw SQL → UNION 拿 admin api_key → bearer
- 调试头泄露 ETS / FPX 说明；FPX 帧 CRC16 对错误帧回显 → GF(2) 解 nonce
- `read_ets` 拿 erlang_cookie；`eval` 执行 `System.cmd("/readflag", [])`

## 解题思路

1. 恢复路由表，SQLi 导出 users.api_key 并登录。
2. 带 debug 头读协议；对错误 CRC 零载荷帧收集 oracle，解 128-bit nonce。
3. 解密 FPX，读 secrets，eval 读 flag。

## 关键代码/payload

```text
# UNION 四列注入导出 api_key（示意）
# CRC oracle: 长度 0..16 错误帧 → 服务端 expected CRC → 线性方程组
```

## 参考链接

- https://xz.aliyun.com/news/93039
