---
title: "日志系统"
competition: "强网杯"
year: 2025
category: "Web"
tags:
  - "PHP `$_GET` 数组与 QUERY_STRING 解析差异"
  - "路径拼接写文件 → webshell"
  - "内网 JBoss Remoting Unified Invoker RCE"
sources:
  - "https://blog.wm-team.cn/index.php/archives/87/"
---
# 日志系统

## 题目信息
- 赛事：强网杯 2025 初赛
- 分类：Web

## 考点
- PHP `$_GET` 数组与 QUERY_STRING 解析差异
- 路径拼接写文件 → webshell
- 内网 JBoss Remoting Unified Invoker RCE

## 解题思路
1. 前端校验要求 `timestamp[year/month/day]` 顺序与纯数字；正则只匹配字母键名，可用数字键绕过拼出 `.php` 文件名（如 `2025101.php`）。
2. POST `content` 写入 `upload/` 下文件，得到 PHP shell。
3. 主机上另有旧版 JBoss；通过代理 + `jboss_remoting_unified_invoker_rce` 一类利用拿到高权限，再按时间找深层路径中的 flag。

## 关键代码/payload
```http
/upload/?timestamp[year]=2025&timestamp[month]=10&timestamp[day]=1.php  (+ POST content=<?php ... ?>)
```

## 参考链接
- https://blog.wm-team.cn/index.php/archives/87/

> 本文为对公开 writeup 的归纳总结，版权归原作者所有；请务必阅读原文核对细节。
