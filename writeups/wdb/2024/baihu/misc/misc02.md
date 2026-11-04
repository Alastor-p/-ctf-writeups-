---
title: misc02
competition: 网鼎杯
year: 2024
category: Misc
tags: [白虎, gtp, aes-ecb]
sources:
  - https://mp.weixin.qq.com/s/5Xet54leUqVOeMYzTX0ROw
  - https://sechub.in/view/2964737
  - https://www.cnblogs.com/backlion/p/18527653
  - https://github.com/CTF-Archives/2024-wdb-baihu
---

# misc02

## 题目信息

- 赛事：第四届网鼎杯 2024 线上资格赛 · 白虎组
- 分类：Misc
- 题面：运营商被打之后留下的流量，另附 `encrypted.py`。见 [CTF-Archives](https://github.com/CTF-Archives/2024-wdb-baihu)。

## 考点

- GTP 头后面的载荷才是密文
- AES-ECB，密钥由 TEID 扩展而来

## 解题思路

附件脚本把一个整数 key `pack` 成 4 字节再右侧补零到 16 字节，对明文做 AES-ECB（脚本里用空格补齐到分组）。流量里 TEID 后面的字节就是按这个脚本加密的。公开做法是把每个报文的 TEID 当成 key，分别解请求和响应。解出来的明文字段里包含 flag。

## 关键代码/payload

```text
key = struct.pack('>I', teid).ljust(16, b'\x00')
AES.new(key, AES.MODE_ECB).decrypt(payload_after_teid)
```

## 参考链接

- https://sechub.in/view/2964737
- https://www.cnblogs.com/backlion/p/18527653
- https://github.com/CTF-Archives/2024-wdb-baihu

> 本文为对公开 writeup 的归纳总结，版权归原作者所有；请务必阅读原文核对细节。
