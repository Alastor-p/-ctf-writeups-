---
title: misc01
competition: 网鼎杯
year: 2024
category: Misc
tags: [青龙, diameter, ecgi, md5]
sources:
  - https://mp.weixin.qq.com/s/HhL4lqcL_3EeYg1TDeBOKg
  - https://cn-sec.com/archives/3331560.html
  - https://www.cnblogs.com/backlion/p/18527653
  - https://github.com/CTF-Archives/2024-wdb-qinglong
---

# misc01

## 题目信息

- 赛事：第四届网鼎杯 2024 线上资格赛 · 青龙组
- 分类：Misc
- 题面：流量取证。定位信息泄露，flag 是该位置信息的 32 位 MD5。见 [CTF-Archives 青龙题单](https://github.com/CTF-Archives/2024-wdb-qinglong)。

## 考点

- Diameter 信令
- E-UTRAN Cell Global Identity / ECGI

## 解题思路

包的数量不多，过滤 Diameter。在 AVP 里找 `Location-Information`（公开文也写成 location-information）。其中一段十六进制被解释成 ECGI，用来标识用户注册的小区。题面要求对这段位置信息做 32 位 MD5。

几篇转载给出的 MD5 和是否带 `wdflag{}` 并不一致，摘要不收录具体 flag，按自己流量里的 ECGI 字段重算。

## 关键代码/payload

```text
过滤 Diameter → AVP Location-Information / ECGI → MD5
```

## 参考链接

- https://mp.weixin.qq.com/s/HhL4lqcL_3EeYg1TDeBOKg
- https://cn-sec.com/archives/3331560.html
- https://www.cnblogs.com/backlion/p/18527653
- https://github.com/CTF-Archives/2024-wdb-qinglong

> 本文为对公开 writeup 的归纳总结，版权归原作者所有；请务必阅读原文核对细节。
