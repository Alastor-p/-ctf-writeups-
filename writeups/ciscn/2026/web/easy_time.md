---
title: easy_time
competition: CISCN&长城杯半决赛
year: 2026
category: Web
tags: ['flask', 'ssrf', 'zip-slip', 'awdp']
sources:
  - 'https://www.cnblogs.com/lee0/p/19759628'
  - 'https://lengkur.github.io/2026/04/15/wp/ciscn2026/easy_time/'
---

# easy_time

## 题目信息

- 分类：WEB / AWDP
- 容器：Flask:5000 对外 + 内网 Apache PHP:80（supervisor）
- 登录：弱口令 `admin` / 哈希对应口令（公开 WP 指出 `secret`）

## 考点

- 头像远程拉取：仅限 http(s)，无 SSRF 主机过滤 → 打内网 80
- 插件 ZIP 解压：`os.path.join(dest, info.filename)` **无规范化** → Zip Slip 写任意路径

## 解题思路

### Break

1. 登录后上传恶意 ZIP，条目名如 `../../../var/www/html/shell.php` 写入 Web 根。
2. 头像 SSRF 访问 `http://127.0.0.1/shell.php?1=…`（或同类）执行；`find` 定位 flag。

### Fix（公开讨论）

- 禁用/严格限制远程头像；解压前 `realpath` + 前缀校验；加固 session。

## 关键代码/payload

```python
# Zip Slip 条目示意
zip_entry_name = "../../../var/www/html/shell.php"
# SSRF avatar URL → http://127.0.0.1/shell.php?...
```

## 参考链接

- https://www.cnblogs.com/lee0/p/19759628
- https://lengkur.github.io/2026/04/15/wp/ciscn2026/easy_time/
