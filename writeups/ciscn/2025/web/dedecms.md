---
title: "dedecms"
competition: "全国大学生信息安全竞赛"
year: 2025
category: "Web"
tags:
  - "织梦 CMS"
  - "注册用户信息泄露/撞库弱口令"
  - "后台上传拿 shell"
sources:
  - "https://luo-kaihong.github.io/p/2025-ciscn%E5%88%9D%E8%B5%9B/"
  - "https://godownio.github.io/2025/12/20/2025-ciscn-chu-sai-wp-by-yp0int/"
---
# dedecms

## 题目信息
- 赛事：CISCN 2025 初赛
- 分类：Web

## 考点
- 织梦 CMS
- 注册用户信息泄露/撞库弱口令
- 后台上传拿 shell

## 解题思路
1. 前台注册/枚举发现用户 `Aa123456789`，密码同用户名可从 `/dede/login.php` 进后台。
2. 在档案文档等上传点改 MIME 传马，命令执行读 flag。

## 关键代码/payload
原文未给出可摘录的短代码，请参阅参考链接中的完整 exploit。

## 参考链接
- https://luo-kaihong.github.io/p/2025-ciscn%E5%88%9D%E8%B5%9B/
- https://godownio.github.io/2025/12/20/2025-ciscn-chu-sai-wp-by-yp0int/

> 本文为对公开 writeup 的归纳总结，版权归原作者所有；请务必阅读原文核对细节。
