---
title: "PTer"
competition: "强网杯"
year: 2025
category: "Web"
tags:
  - "BT Tracker 风格 PHP 应用"
  - "SQL 注入（`ip` 来自可伪造的 XFF）"
  - "Host 校验绕过"
  - "附件目录劫持 + LFI"
sources:
  - "https://cn-sec.com/archives/4597169.html"
---
# PTer

## 题目信息
- 赛事：强网杯 2025 初赛
- 分类：Web

## 考点
- BT Tracker 风格 PHP 应用
- SQL 注入（`ip` 来自可伪造的 XFF）
- Host 校验绕过
- 附件目录劫持 + LFI

## 解题思路
1. announce 接口要求合法 `info_hash`/`passkey`/`peer_id` 等参数。
2. 查询 peers 时把 `$ip` 直接拼进 SQL；IP 取自可被 `X-Forwarded-For` 影响的值。
3. 需把 Host 改成题目给出的 tracker 域名（如 `pter.qwb.local`）以通过校验。
4. 后续通过改附件目录 + 上传 + 文件包含爆破文件名拿到 shell/flag。

## 关键代码/payload
原文未给出可摘录的短代码，请参阅参考链接中的完整 exploit。

## 参考链接
- https://cn-sec.com/archives/4597169.html

> 本文为对公开 writeup 的归纳总结，版权归原作者所有；请务必阅读原文核对细节。
