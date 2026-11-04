---
title: misc03
competition: 网鼎杯
year: 2024
category: Misc
tags: [朱雀, crc32, veracrypt, rsa]
sources:
  - https://cn-sec.com/archives/3363175.html
  - https://mp.weixin.qq.com/s/Icf6QC1eCsz95vFdDpdm7g
  - https://www.cnblogs.com/backlion/p/18527653
  - https://github.com/CTF-Archives/2024-wdb-zhuque
---

# misc03

## 题目信息

- 赛事：第四届网鼎杯 2024 线上资格赛 · 朱雀组
- 分类：Misc
- 题面：PNG 里藏了加密卷。见 [CTF-Archives](https://github.com/CTF-Archives/2024-wdb-zhuque)。

## 考点

- binwalk / foremost 分离
- 6 字节未知明文的 CRC32 碰撞
- VeraCrypt 挂载
- 加密的 RSA 私钥解 `flag.txt`

## 解题思路

PNG 尾部还能再分出压缩包，其中若干成员只有 6 字节，需要密码。公开做法是对这几个成员的 CRC32 做碰撞，把碰撞出的短串拼成口令。两篇转载拼出来的口令一个写成 `This_WD_011cryptpW`，一个写成 `This_WD_010cryptPw`，差在个别字符，以本地 CRC 为准，这里不指定哪一个。

用该口令解开压缩包，文档名指向 VeraCrypt。同一口令挂载后得到 `secret.key`（加密的 PKCS#8 私钥）和 `flag.txt`，用私钥解密即可。

## 关键代码/payload

```text
binwalk 分离 → 6 字节成员 CRC32 碰撞 → 拼口令
VeraCrypt 挂载 → 加密 RSA 私钥解 flag.txt
```

## 参考链接

- https://cn-sec.com/archives/3363175.html
- https://www.cnblogs.com/backlion/p/18527653

> 本文为对公开 writeup 的归纳总结，版权归原作者所有；请务必阅读原文核对细节。
