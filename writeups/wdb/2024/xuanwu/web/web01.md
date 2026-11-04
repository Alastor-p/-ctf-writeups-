---
title: web01
competition: 网鼎杯
year: 2024
category: Web
tags: [玄武, eyoucms, thinkphp, unserialize]
sources:
  - https://www.ctfiot.com/214152.html
  - https://sechub.in/view/2966475
  - https://cn-sec.com/archives/3379949.html
  - https://blog.xmcve.com/2024/11/05/%E7%BD%91%E9%BC%8E%E6%9D%AF-2024-Writeup/
---

# web01

## 题目信息

- 赛事：第四届网鼎杯 2024 线上资格赛 · 玄武组
- 分类：Web
- 题面：EyouCMS。`/data/conf/version.txt` 为 1.6.5。后台 `/login.php`。

## 考点

- 后台弱口令 `admin` / `admin`
- `dfvalue` 反序列化（ThinkPHP 5.0.24 链）
- `dfvalue` 长度上限，以及 `dtype` 过滤用数组绕过

## 解题思路

首页图标或源码都能看出是 EyouCMS。公开 WP 登录后台后，利用点在字段编辑：`channel_edit` 会反序列化 `dfvalue`。直接套网上的 TP 5.0.24 链有两个坑：`dfvalue` 限长约 500，所以要用缩短过的链；`arctype_edit` / `channel_edit` 会滤掉反序列化需要的字符。

绕过方式是新增字段时把 `dtype` 设成 `region`，编辑时改成 `dtype[]=region`，把缩短链放进 `dfvalue`。再访问

`/login.php?m=admin&c=Field&a=channel_edit&channel_id=-99&id=<新建字段>&_ajax=1`

触发反序列化，写出 webshell（公开文中的文件名带固定 md5 前缀）。完整 POP 链见原文和他们引用的 CN-SEC 分析，这里不贴对象图。

## 关键代码/payload

```text
POST 字段：dtype[]=region，dfvalue=<缩短后的 TP 5.0.24 链>
GET /login.php?m=admin&c=Field&a=channel_edit&channel_id=-99&id=<id>&_ajax=1
```

## 参考链接

- https://www.ctfiot.com/214152.html
- https://sechub.in/view/2966475
- https://cn-sec.com/archives/3379949.html
- https://blog.xmcve.com/2024/11/05/%E7%BD%91%E9%BC%8E%E6%9D%AF-2024-Writeup/

> 本文为对公开 writeup 的归纳总结，版权归原作者所有；请务必阅读原文核对细节。
