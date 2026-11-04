---
title: misc02
competition: 网鼎杯
year: 2024
category: Misc
tags: [朱雀, jar, aes, base64]
sources:
  - https://cn-sec.com/archives/3363175.html
  - https://mp.weixin.qq.com/s/Icf6QC1eCsz95vFdDpdm7g
  - https://www.cnblogs.com/backlion/p/18527653
  - https://github.com/CTF-Archives/2024-wdb-zhuque
---

# misc02

## 题目信息

- 赛事：第四届网鼎杯 2024 线上资格赛 · 朱雀组
- 分类：Misc
- 题面：盲盒 jar，要求 JDK 1.8。见 [CTF-Archives](https://github.com/CTF-Archives/2024-wdb-zhuque)。

## 考点

- jadx / IDEA 看 AES
- 密钥写在源码里
- 多层 Base64 里夹着真正的密文

## 解题思路

程序直接跑进不去。反编译能看到 `SecretKeySpec(..., "AES")`，密钥字符串是 `Y4SuperSecretKey`。类里有很多 Base64 常量，逐段解开，其中一段才是 AES 密文。公开 WP 用在线 AES 解密得到 flag。

玄武组 reverse02 的公开文章里也出现过同一个密钥串和 jar 形态。题面不同（盲盒 vs 逆向题），本篇只按朱雀 misc02 的描述写，不把两组附件当成同一个文件。

## 关键代码/payload

```text
AES key = "Y4SuperSecretKey"
# 多个 Base64 常量里挑出真正的密文再解密
```

## 参考链接

- https://cn-sec.com/archives/3363175.html
- https://www.cnblogs.com/backlion/p/18527653
- https://github.com/CTF-Archives/2024-wdb-zhuque

> 本文为对公开 writeup 的归纳总结，版权归原作者所有；请务必阅读原文核对细节。
