---
title: reverse01
competition: 网鼎杯
year: 2024
category: Reverse
tags: [青龙, apk, sm4, so]
sources:
  - https://mp.weixin.qq.com/s/HhL4lqcL_3EeYg1TDeBOKg
  - https://cn-sec.com/archives/3331560.html
  - https://sechub.in/view/2962999
  - https://github.com/CTF-Archives/2024-wdb-qinglong
---

# reverse01

## 题目信息

- 赛事：第四届网鼎杯 2024 线上资格赛 · 青龙组
- 分类：Reverse
- 题面：Android 安装包。题单见 [CTF-Archives](https://github.com/CTF-Archives/2024-wdb-qinglong)。

## 考点

- jadx 定位 `MainActivity`，再跟进 native `check`
- 与标准 SM4 略有差别的分组密码
- 密钥后半段的字节序

## 解题思路

Java 层被混淆，有用逻辑在 native。公开 WP 把 so 丢进 IDA，认出 SM4 形态的轮函数，但和标准实现有出入。密文和 key 都在 so 里：key 后半是字符串 `Z0099864`，要按端序倒成 `4689900Z` 再拼到前半。用拼好的 key 解出密文即 flag。标准库直接套可能对不齐，以逆向出来的轮函数为准。

## 关键代码/payload

```text
key 后半 "Z0099864"[::-1] == "4689900Z"
SM4_decrypt(key, ciphertext)
```

## 参考链接

- https://mp.weixin.qq.com/s/HhL4lqcL_3EeYg1TDeBOKg
- https://cn-sec.com/archives/3331560.html
- https://sechub.in/view/2962999

> 本文为对公开 writeup 的归纳总结，版权归原作者所有；请务必阅读原文核对细节。
