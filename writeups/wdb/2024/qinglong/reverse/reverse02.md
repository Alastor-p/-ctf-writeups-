---
title: reverse02
competition: 网鼎杯
year: 2024
category: Reverse
tags: [青龙, aes, custom-base64, xor]
sources:
  - https://mp.weixin.qq.com/s/HhL4lqcL_3EeYg1TDeBOKg
  - https://cn-sec.com/archives/3331560.html
  - https://sechub.in/view/2962999
  - https://www.cnblogs.com/backlion/p/18527653
  - https://github.com/CTF-Archives/2024-wdb-qinglong
---

# reverse02

## 题目信息

- 赛事：第四届网鼎杯 2024 线上资格赛 · 青龙组
- 分类：Reverse
- 题面：无壳 ELF。输入 40 字节，前缀 `wdflag{`，末字节 `}`，中间 32 字节分四段检查。题单称「四大护法」，见 [CTF-Archives](https://github.com/CTF-Archives/2024-wdb-qinglong)。

## 考点

- 逐字节乘 2
- 与固定串异或
- 换表 Base64
- AES-ECB

## 解题思路

`main` 把花括号里的 32 字节切成四段，每段 8 字节（最后一段再参与一次 16 字节 AES）。公开伪代码的顺序是：

1. 前 8 字节乘 2，对比常量；
2. 接下来 8 字节与 `"XorrLord"` 异或；
3. 再 8 字节做换表 Base64，目标串形如 `QYGyBYKyA2K`，码表相对标准表有旋转；
4. 最后一段配固定填充后，用密钥 `"AesMasterAesMast"` 做 AES-ECB，对比 16 字节常量。

从第 4 段往第 1 段解密再拼回去。不同文章贴出的常量字节并不相同，flag 也就对不上，按自己 IDA 里的 `s2` / `v11` / `v4` 算，不要混用别的附件的中间结果。

## 关键代码/payload

```text
part1 = s2[i] // 2
part2 = v11[i] XOR "XorrLord"
part3 = base64_decode(custom_table, "QYGyBYKyA2K")
part4 = AES_ECB_decrypt(key="AesMasterAesMast", block=v4)[:8]
```

## 参考链接

- https://mp.weixin.qq.com/s/HhL4lqcL_3EeYg1TDeBOKg
- https://cn-sec.com/archives/3331560.html
- https://sechub.in/view/2962999
- https://www.cnblogs.com/backlion/p/18527653

> 本文为对公开 writeup 的归纳总结，版权归原作者所有；请务必阅读原文核对细节。
