---
title: "SecretVault"
competition: "强网杯"
year: 2025
category: "Web"
tags:
  - "Go 鉴权网关 + Python Flask/业务后端"
  - "HTTP/1.1 hop-by-hop：`Connection` 列出的头在转发时被删除"
  - "伪造/保留 `X-User: 0` 以读取 admin Vault"
sources:
  - "https://blog.wm-team.cn/index.php/archives/87/"
  - "https://cn-sec.com/archives/4592147.html"
---
# SecretVault

## 题目信息
- 赛事：强网杯 2025 初赛
- 分类：Web

## 考点
- Go 鉴权网关 + Python Flask/业务后端
- HTTP/1.1 hop-by-hop：`Connection` 列出的头在转发时被删除
- 伪造/保留 `X-User: 0` 以读取 admin Vault

## 解题思路
1. 服务启动时创建 uid=0 的 admin，并把 flag 以 Fernet 加密成 VaultEntry 绑在 admin 上。
2. 登录成功后访问内网 `/sign` 拿 token；Go 侧验 token，但真正决定 Python 侧身份的是转发时的 `X-User`。
3. 网关默认会把 `X-User` 设成 anonymous；若请求里写 `Connection: close, X-User`，按规范 hop-by-hop 头会在转发中被去掉，网关 `Set` 的值也可能因同名头处理差异而丢失。
4. 最终让 Python 以 uid=0 身份读到 flag 条目（具体细节以原文实验为准）。

## 关键代码/payload
```http
Connection: close, X-User
```

## 参考链接
- https://blog.wm-team.cn/index.php/archives/87/
- https://cn-sec.com/archives/4592147.html

> 本文为对公开 writeup 的归纳总结，版权归原作者所有；请务必阅读原文核对细节。
