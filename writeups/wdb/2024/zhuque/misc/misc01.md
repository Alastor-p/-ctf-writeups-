---
title: misc01
competition: 网鼎杯
year: 2024
category: Misc
tags: [朱雀, manchester, zip, pixeljihad]
sources:
  - https://cn-sec.com/archives/3363175.html
  - https://carlzhang.xyz/technology/blog_CTF_2024WangDingCup.html
  - https://mp.weixin.qq.com/s/Icf6QC1eCsz95vFdDpdm7g
  - https://www.cnblogs.com/backlion/p/18527653
  - https://github.com/CTF-Archives/2024-wdb-zhuque
---

# misc01

## 题目信息

- 赛事：第四届网鼎杯 2024 线上资格赛 · 朱雀组
- 分类：Misc
- 题面：一长串 `0`/`1`。题单故事是卫星截获的信号。见 [CTF-Archives](https://github.com/CTF-Archives/2024-wdb-zhuque)。

## 考点

- 差分曼彻斯特
- ZIP 固定步长里夹了多余字节
- 弱口令压缩包
- PNG 尾部 Base64，以及 PixelJihad 隐写

## 解题思路

2020 年朱雀组用过曼彻斯特，这串比特也按这个方向试。公开脚本比较相邻两个电平：相同记 0、不同记 1（具体相位各文略有差别）。解码后能看到 `504B`，即 ZIP。

ZIP 被按固定周期插入了垃圾字节。Carl Zhang 用正则剔干扰；另一篇按「每 22 字节去掉末尾 6 字节」或「44 字节里去掉 12 个」修复，头部 `504B0304` 用来校验步长。修完需要密码，公开文章猜中 `12345678`。

包内是 PNG。尾部一段像 Base64，解出来是 `ppaasswd`。用 PixelJihad（`sekao.net/pixeljihad`）和这个口令抽出 flag。不同文章的 flag 字符串不要混用，以自己解出来的图为准。

## 关键代码/payload

```text
差分曼彻斯特 → 出现 504B0304
每 22 字节去掉尾部 6 字节（步长以本地修复为准）
zip 密码 12345678 → PNG 尾部 Base64「ppaasswd」→ PixelJihad
```

## 参考链接

- https://cn-sec.com/archives/3363175.html
- https://carlzhang.xyz/technology/blog_CTF_2024WangDingCup.html
- https://www.cnblogs.com/backlion/p/18527653

> 本文为对公开 writeup 的归纳总结，版权归原作者所有；请务必阅读原文核对细节。
