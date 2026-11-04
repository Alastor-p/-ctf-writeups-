---
title: misc03
competition: 网鼎杯
year: 2024
category: Misc
tags: [青龙, pcap, http, attribution]
sources:
  - https://mp.weixin.qq.com/s/HhL4lqcL_3EeYg1TDeBOKg
  - https://cn-sec.com/archives/3331560.html
  - https://www.cnblogs.com/backlion/p/18527653
  - https://github.com/CTF-Archives/2024-wdb-qinglong
---

# misc03

## 题目信息

- 赛事：第四届网鼎杯 2024 线上资格赛 · 青龙组
- 分类：Misc
- 题面：服务器被攻击，流量里要找出攻击者 IP。flag 格式是 `wdflag{攻击IP}`。见 [CTF-Archives 青龙题单](https://github.com/CTF-Archives/2024-wdb-qinglong)。

## 考点

- HTTP 流量里区分上传木马的源地址

## 解题思路

公开 WP 的做法很短：包里主要是 HTTP。顺着 POST 上传找 webshell（文中提到 `hacker.php` 一类文件名），候选源 IP 有好几个，逐个对照上传是否真的把马写进去。被多篇转载写成答案的攻击源是 `39.168.5.60`，flag 即 `wdflag{39.168.5.60}`。

## 关键代码/payload

```text
HTTP POST 上传 → 确认 webshell 文件名 → 源 IP
```

## 参考链接

- https://mp.weixin.qq.com/s/HhL4lqcL_3EeYg1TDeBOKg
- https://cn-sec.com/archives/3331560.html
- https://www.cnblogs.com/backlion/p/18527653

> 本文为对公开 writeup 的归纳总结，版权归原作者所有；请务必阅读原文核对细节。
