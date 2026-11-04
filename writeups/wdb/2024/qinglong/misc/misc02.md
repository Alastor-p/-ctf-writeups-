---
title: misc02
competition: 网鼎杯
year: 2024
category: Misc
tags: [青龙, memory-forensics, 7z, sm4]
sources:
  - https://mp.weixin.qq.com/s/Icf6QC1eCsz95vFdDpdm7g
  - https://www.cnblogs.com/backlion/p/18527653
  - https://github.com/CTF-Archives/2024-wdb-qinglong
---

# misc02

## 题目信息

- 赛事：第四届网鼎杯 2024 线上资格赛 · 青龙组
- 分类：Misc
- 题面：机器变慢，磁盘上留下加密代码；恢复未删干净的内容，解一个 TXT 压缩包。附件是无后缀文件。题单见 [CTF-Archives](https://github.com/CTF-Archives/2024-wdb-qinglong)。

## 考点

- Linux 内存镜像里搜字符串，而不是硬靠 Volatility
- PNG 的 base64 在内存里分段
- 7z 掩码爆破
- 从字节码还原 SM4 密钥变换

## 解题思路

`strings` 能看出 Ubuntu 22.04 镜像，以及用户目录 `/home/ccc/Desktop/`。公开 WP 试过按 6.5 内核做 Volatility3 符号，扫不出有用结果，于是改在十六进制编辑器里搜。

桌面命令历史里有 `base64 xxx.png > xxx.txt`。PNG 头的 base64 是 `iVBORw0KGgo`，按这个锚点把被拆开的 base64 拼回去（下一段往往贴着上一段的尾巴）。`zsteg` 即使图不完整也能读出形如 `Y3p_Ke9_1s_?????` 的提示。镜像末尾还有 7z 头 `37 7A BC AF 27 1C`，按这个掩码爆破压缩包。

解出来的文本是一段 Python 字节码：`key_encode` 把相邻字节做异或，再和原 key 异或，得到 16 字节 SM4 密钥；`encrypted_data` 用该密钥解密即 flag。完整字节码和密钥以原文为准，这里不抄。

## 关键代码/payload

```text
strings → /home/ccc/Desktop → 拼接 iVBORw0KGgo...
zsteg hint Y3p_Ke9_1s_????? → 7z
SM4(key_encode(key), encrypted_data)
```

## 参考链接

- https://mp.weixin.qq.com/s/Icf6QC1eCsz95vFdDpdm7g
- https://www.cnblogs.com/backlion/p/18527653
- https://github.com/CTF-Archives/2024-wdb-qinglong

> 本文为对公开 writeup 的归纳总结，版权归原作者所有；请务必阅读原文核对细节。
