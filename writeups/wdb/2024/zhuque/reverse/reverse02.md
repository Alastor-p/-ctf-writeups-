---
title: reverse02
competition: 网鼎杯
year: 2024
category: Reverse
tags: [朱雀, vmp, ransomware, aes]
sources:
  - https://sechub.in/view/2965877
  - https://github.com/CTF-Archives/2024-wdb-zhuque
---

# reverse02

## 题目信息

- 赛事：第四届网鼎杯 2024 线上资格赛 · 朱雀组
- 分类：Reverse
- 题面：勒索场景。样本套了 VMP，附件见 [CTF-Archives](https://github.com/CTF-Archives/2024-wdb-zhuque)。

## 考点

- 不脱 VMP，靠字符串找到释放逻辑
- 反调试：先跑起来再下断
- 异或脱出 ELF，ELF 里是 AES

## 解题思路

壳不好脱。公开 WP 直接搜字符串，能看到勒索和加密相关字样。跟 `svchost.exe` 发现一段异或，沙箱里也能观察到释放或注入。样本会查断点，所以先运行、再立刻断。

把 `0x3650048` 处的数据异或出来是 ELF。ELF 对文件做 AES，导出的 key 为 `3b7e151638aed2a6bbf7158819cf4f3c`。ChaMd5 之后用 CyberChef 再配合异或爆破得到 flag。完整样本偏移以原文为准。

## 关键代码/payload

```text
异或 0x3650048 处数据 → ELF
AES key = 3b7e151638aed2a6bbf7158819cf4f3c
```

## 参考链接

- https://sechub.in/view/2965877

> 本文为对公开 writeup 的归纳总结，版权归原作者所有；请务必阅读原文核对细节。
