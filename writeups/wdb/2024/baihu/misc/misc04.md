---
title: misc04
competition: 网鼎杯
year: 2024
category: Misc
tags: [白虎, zip, fake-encryption, stego]
sources:
  - https://mp.weixin.qq.com/s/5Xet54leUqVOeMYzTX0ROw
  - https://sechub.in/view/2964737
  - https://github.com/CTF-Archives/2024-wdb-baihu
---

# misc04

## 题目信息

- 赛事：第四届网鼎杯 2024 线上资格赛 · 白虎组
- 分类：Misc
- 题面：三个分片文件，拼起来才是完整容器。见 [CTF-Archives](https://github.com/CTF-Archives/2024-wdb-baihu)。

## 考点

- 文件拼接后 binwalk 出两层压缩包
- ZIP 伪加密
- 已知掩码爆破，以及 JPG 里再拆 PNG、改宽高

## 解题思路

`cat 1 2 3 > 1.zip` 之后 binwalk 能看到两个压缩包。其中一个是伪加密，解开得到图，图里是 flag 的后半段（文中说镜像后可读）。

另一个压缩包的提示是 `!@#QQQ0010flag****`，只掩码爆破后四位。出来的 JPG 里还能再分离一张 PNG，宽高不对，爆破宽高后读出 flag 前半段。两半拼在一起。

## 关键代码/payload

```text
cat 1 2 3 > merged
# 伪加密 ZIP → 后半 flag
# 掩码 !@#QQQ0010flag???? → JPG 内 PNG，修正宽高 → 前半 flag
```

## 参考链接

- https://mp.weixin.qq.com/s/5Xet54leUqVOeMYzTX0ROw
- https://sechub.in/view/2964737

> 本文为对公开 writeup 的归纳总结，版权归原作者所有；请务必阅读原文核对细节。
