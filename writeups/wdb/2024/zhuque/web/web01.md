---
title: web01
competition: 网鼎杯
year: 2024
category: Web
tags: [朱雀, nodejs, type-confusion, apache, cve-2023-25690]
sources:
  - https://blog.huggy.moe/posts/2024/9-wdctf-web01-writeup/
  - https://github.com/CTF-Archives/2024-wdb-zhuque
---

# web01

## 题目信息

- 赛事：第四届网鼎杯 2024 线上资格赛 · 朱雀组
- 分类：Web
- 题面：已停用的博客。flag 在管理员文章里，管理员密码是随机的。归档 README 把 Web-01 题面写成 None，但这篇 WP 明确是朱雀组。

## 考点

- 查询参数数组绕过 `username === "admin"`
- Apache 2.4.53 强制把 `Auth` 设成 `guest`
- CVE-2023-25690：`mod_rewrite` + `mod_proxy` 请求走私，把 `Auth: admin` 送进后端

## 解题思路

`/search` 从 `req.query` 取出 `username`，只在它严格等于字符串 `"admin"` 时拒绝。Map 的键比较允许数组，所以 `username[]=admin` 能列出管理员文章的 uuid。前端走的是 `/dosearch/username/...` 伪静态，数组参数要直接打 `/search`。

`/post` 要求 `req.role === "admin"`，而 `app.js` 把 `req.headers.auth` 赋给 `req.role`。`httpd.conf` 里 `RequestHeader set Auth "guest"` 会盖掉客户端自己带的头，改大小写也没用。镜像是 `httpd:2.4.53`，RewriteRule 把路径代理到 Node。这落在 CVE-2023-25690：在 URL 里塞入 `\r\nAuth: admin\r\n`，让代理拆出的后端请求带上管理员角色，再读那篇未公开的 flag 文章。

公开文中的响应体是占位 `wdflag{test_flag}`，不是比赛 flag。

## 关键代码/payload

```text
GET /search?username[]=admin
# httpd 2.4.53 RewriteRule [P]
GET /dopost/id/<uuid>%20HTTP/1.1%0d%0aAuth:%20admin%0d%0a%0d%0aGET%20/SMUGGLED HTTP/1.1
```

## 参考链接

- https://blog.huggy.moe/posts/2024/9-wdctf-web01-writeup/
- https://github.com/CTF-Archives/2024-wdb-zhuque

> 本文为对公开 writeup 的归纳总结，版权归原作者所有；请务必阅读原文核对细节。
