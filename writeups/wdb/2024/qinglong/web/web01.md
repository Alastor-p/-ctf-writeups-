---
title: web01
competition: 网鼎杯
year: 2024
category: Web
tags: [青龙, jwt, rs256, flask-session, xxe, ssrf]
sources:
  - https://k1te.cn/p/2024%E7%BD%91%E9%BC%8E%E6%9D%AF%E9%9D%92%E9%BE%99%E7%BB%84web%E5%85%A8wp/
  - https://www.cnblogs.com/backlion/p/18527653
  - https://www.caterpie771.cn/archives/339
---

# web01

## 题目信息

- 赛事：第四届网鼎杯 2024 线上资格赛 · 青龙组
- 分类：Web
- 题面：登录后同时下发 JWT 和 Flask session。非 admin 用户名都能登进去，`admin` 这个名字在登录口被拒绝。

## 考点

- RS256：用两枚签名恢复公钥，且一个素因子极小
- emoji 映射成 shell，读出 `SECRET_KEY`
- 伪造 Flask session 的 `role=admin`
- SSRF 绕过域名白名单后，UTF-16 的 XXE 读 PHP 文件

## 解题思路

任意非空用户名会签一张 `{"username": ...}` 的 RS256 JWT。公开 WP 用两张游客票（DownUnderCTF 2021 那类 `rsa_sign2n` / JWT-Key-Recovery）算出公钥，并发现 `q = 37`，于是模数可以直接分解，伪造 `username=admin`。

Game 路由只对 admin 开放。输入若不含可打印字符（空格除外），会按表把 emoji 换成字母再 `os.popen`。公开文章用这张表把命令拼成读取 `/app` 源码，从而拿到 `SECRET_KEY`（文中为 `36f8efbea152e50b23290e0ed707b4b0`）。本地用同一密钥签 `session['role']='admin'`。

上传接口把文件交给本机 `upload.php`。`view_uploads` 要求 path 含 `www.testctf.com`、不能出现 `127.0.0.1`，filepath 必须带 `/var/www/html/uploads/` 且不能有 `.`。公开绕法是 `www.testctf.com@0.0.0.0`（或 `localhost`）。回显提到 XML 解析失败，于是上传 XXE；关键字过滤用 `iconv` 转成 UTF-16 再读 `flag.php`。

## 关键代码/payload

```text
两张 RS256 → 恢复 n，q=37 → 伪造 username=admin
emoji 命令读出 SECRET_KEY → 伪造 role=admin
path=www.testctf.com@0.0.0.0
XXE: php://filter/convert.base64-encode/resource=flag.php （UTF-16）
```

## 参考链接

- https://k1te.cn/p/2024%E7%BD%91%E9%BC%8E%E6%9D%AF%E9%9D%92%E9%BE%99%E7%BB%84web%E5%85%A8wp/
- https://www.cnblogs.com/backlion/p/18527653
- https://www.caterpie771.cn/archives/339

> 本文为对公开 writeup 的归纳总结，版权归原作者所有；请务必阅读原文核对细节。
