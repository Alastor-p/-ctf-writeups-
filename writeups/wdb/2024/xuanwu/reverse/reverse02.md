---
title: reverse02
competition: 网鼎杯
year: 2024
category: Reverse
tags: [玄武, jar, aes, base64]
sources:
  - https://www.ctfiot.com/214152.html
  - https://sechub.in/view/2966475
  - https://blog.xmcve.com/2024/11/05/%E7%BD%91%E9%BC%8E%E6%9D%AF-2024-Writeup/
---

# reverse02

## 题目信息

- 赛事：第四届网鼎杯 2024 线上资格赛 · 玄武组
- 分类：Reverse
- 题面：一个 jar。ChaMd5 与星盟的玄武 web 题写在同一篇里，因此把这篇逆向也归在玄武组。

## 考点

- jadx / jd-gui
- 自定义 Base64 形态的编码
- 源码里的 AES 密钥，多段密文里只有一段是 flag

## 解题思路

ChaMd5：jadx 打开后先看到类似 Base64 的例程，全局再搜 AES，密钥就在附近，对各个密文试解密。

星盟同一场的笔记把密钥写成 `Y4SuperSecretKey`，`SecretKeySpec` 的算法名是 `AES`，密文挂在混淆过的字段上。朱雀组 misc02 的公开 WP 也使用这个密钥串。两组题面不同，是否为同一附件无法从文字上断定，解密时以自己的 jar 为准。

## 关键代码/payload

```text
jadx → 搜 AES
SecretKeySpec(key, "AES")
# 星盟笔记中的 key 字符串：Y4SuperSecretKey
```

## 参考链接

- https://www.ctfiot.com/214152.html
- https://sechub.in/view/2966475
- https://blog.xmcve.com/2024/11/05/%E7%BD%91%E9%BC%8E%E6%9D%AF-2024-Writeup/

> 本文为对公开 writeup 的归纳总结，版权归原作者所有；请务必阅读原文核对细节。
