---
title: misc01
competition: 网鼎杯
year: 2024
category: Misc
tags: [白虎, gtp, teid, 5g]
sources:
  - https://mp.weixin.qq.com/s/5Xet54leUqVOeMYzTX0ROw
  - https://sechub.in/view/2964737
  - https://www.cnblogs.com/backlion/p/18527653
  - https://github.com/CTF-Archives/2024-wdb-baihu
---

# misc01

## 题目信息

- 赛事：第四届网鼎杯 2024 线上资格赛 · 白虎组
- 分类：Misc
- 题面：5G / UPF 流量。把恶意报文里的 TEID 按时间拼起来，外面再套 `wdflag{}`。见 [CTF-Archives 白虎题单](https://github.com/CTF-Archives/2024-wdb-baihu)。

## 考点

- GTP-U 的 TEID 字段
- 按出现次数把正常隧道和异常报文分开

## 解题思路

用 tshark 把 `gtp.teid` 倒出来再计数。绝大多数 TEID 只出现一次，有两条（或两个值）明显重复，对应攻击者塞进来的报文。按时间把这两处 TEID 拼成 flag。

ChaMd5 正文把结果打码成 `wdflag{18xxx23xxx}`；另一篇转载写成 `wdflag{2235649299000124}`。两篇对「哪两个 TEID」的表述也不完全一样，以自己 pcap 里统计结果为准。

## 关键代码/payload

```text
tshark -r UPF.cap -e gtp.teid -T fields
# 统计后取出异常 TEID，按时间拼接
```

## 参考链接

- https://mp.weixin.qq.com/s/5Xet54leUqVOeMYzTX0ROw
- https://sechub.in/view/2964737
- https://www.cnblogs.com/backlion/p/18527653

> 本文为对公开 writeup 的归纳总结，版权归原作者所有；请务必阅读原文核对细节。
