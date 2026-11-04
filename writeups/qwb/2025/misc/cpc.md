---
title: "cpc"
competition: "强网杯"
year: 2025
category: "Misc"
tags:
  - "Check Point 远程访问 VPN 任意文件读（CVE-2024-24919）"
  - "审计日志还原配置与线索"
sources:
  - "https://blog.wm-team.cn/index.php/archives/87/"
---
# cpc

## 题目信息
- 赛事：强网杯 2025 初赛
- 分类：Misc

## 考点
- Check Point 远程访问 VPN 任意文件读（CVE-2024-24919）
- 审计日志还原配置与线索

## 解题思路
1. 用公开 PoC 任意读网关文件。
2. 读取 `/var/log/opt/CPsuite-.../fw1/log/*.adtlog` 等审计日志，本地用 `fw log` 解析。
3. 从对象创建记录中提取域、账号、门户路径等拼出 flag 所需信息（以原文为准）。

## 关键代码/payload
原文未给出可摘录的短代码，请参阅参考链接中的完整 exploit。

## 参考链接
- https://blog.wm-team.cn/index.php/archives/87/

> 本文为对公开 writeup 的归纳总结，版权归原作者所有；请务必阅读原文核对细节。
