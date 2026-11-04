---
title: pwn01
competition: 网鼎杯
year: 2024
category: Pwn
tags: [白虎, heap, tcache, free-hook]
sources:
  - https://mp.weixin.qq.com/s/5Xet54leUqVOeMYzTX0ROw
  - https://sechub.in/view/2964737
  - https://sechub.in/view/2966219
  - https://github.com/CTF-Archives/2024-wdb-baihu
---

# pwn01

## 题目信息

- 赛事：第四届网鼎杯 2024 线上资格赛 · 白虎组
- 分类：Pwn
- 题面：增删改查菜单。`edit` 实际只能用一次。题单见 [CTF-Archives](https://github.com/CTF-Archives/2024-wdb-baihu)。

## 考点

- 单字节任意地址写 `\x00`
- unsorted / tcache 残留指针泄漏 libc 和堆
- 改 fd 低字节，把 `__free_hook` 写成 `system`

## 解题思路

ChaMd5 的公开分析：`edit` 不是改堆内容，而是往任意地址写一个 `\x00`，而且只有一次。`free` 进 tcache 或从大块里 `show` 时，用户数据末尾会留下 libc 和堆指针，先把基址算出来。

再利用这次 `\x00` 去改某个已释放块 fd 的最后一个字节，让后续分配重叠到目标附近，把 `__free_hook` 填成 `system`，释放一块内容为 `/bin/sh` 的块。完整堆布局和偏移见原文与先知上的专项分析，本摘要不放 exp。

## 关键代码/payload

```text
show 大块残留 → libc / heap
edit 一次：目标地址附近写 0x00，改 fd 低字节
tcache → __free_hook = system；free("/bin/sh")
```

## 参考链接

- https://sechub.in/view/2964737
- https://sechub.in/view/2966219
- https://xz.aliyun.com/t/16074

> 本文为对公开 writeup 的归纳总结，版权归原作者所有；请务必阅读原文核对细节。
