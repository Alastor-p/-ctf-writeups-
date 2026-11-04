---
title: web03
competition: 网鼎杯
year: 2024
category: Web
tags: [玄武, stego, rsa, ssh]
sources:
  - https://1cepeak.cn/posts/wdb2024-turtle-writeup/
  - https://www.ctfiot.com/214152.html
  - https://sechub.in/view/2966475
  - https://cn-sec.com/archives/3379949.html
  - https://blog.xmcve.com/2024/11/05/%E7%BD%91%E9%BC%8E%E6%9D%AF-2024-Writeup/
---

# web03

## 题目信息

- 赛事：第四届网鼎杯 2024 线上资格赛 · 玄武组
- 分类：Web
- 题面：站点上能扫到 `robots.txt`，里面指向 `wbStego4.bmp`，并给出 SSH 用户名 `root456` 和一段口令。

## 考点

- wbStego4，空密码
- 只对公钥头做字母表反转，Base64 正文不动
- 两素数非常接近的 RSA，分解后登录 SSH

## 解题思路

bmp 用 wbStego4、密码为空抽出一段文字。开头几个字母被做了 `A…Z` 对 `Z…A` 的替换，空格后面的 `AAAAB3NzaC1yc2E…` 已经是正常的 OpenSSH 公钥，不要一起替换。ChaMd5 原文写过「整段都解密」是错的，后来用 `ssh-keygen -l` 核对才改回来。

`ssh-keygen -e -m PKCS8` 转成 PEM，读出模数。`p` 和 `q` 只差几百，yafu 或差量分解都能拆开。用 `e = 65537` 生成私钥，`ssh -i` 以 `root456` 登录。robots 里的 `*111!!` 不是 SSH 口令。

nginx 1.18 的请求走私在公开 WP 里试过，没有借它拿到后续文件。

## 关键代码/payload

```text
wbStego4 空密码
仅 A-Z 与 Z-A 对换公钥头；"ssh-rsa AAAAB3…" 保持原样
分解 n → PEM 私钥 → ssh root456
```

## 参考链接

- https://1cepeak.cn/posts/wdb2024-turtle-writeup/
- https://www.ctfiot.com/214152.html
- https://sechub.in/view/2966475
- https://cn-sec.com/archives/3379949.html
- https://blog.xmcve.com/2024/11/05/%E7%BD%91%E9%BC%8E%E6%9D%AF-2024-Writeup/

> 本文为对公开 writeup 的归纳总结，版权归原作者所有；请务必阅读原文核对细节。
