---
title: vaultcache
competition: 羊城杯
year: 2026
category: Pwn
tags: ['redis-module', 'sds-overflow', 'tcache', 'setjmp', 'protocol-reuse']
sources: ['https://xz.aliyun.com/news/93035']
---

# vaultcache

## 题目信息

- 分类：PWN（HARD）
- 链：`Redis+vaultcache.so → vaultbroker → routeledger → routecouncil → flag`
- ledger/council 二进制与 redisrelay 题同构，可复用协议库

## 考点

- 模块 RDB `RESTORE` 长度检查过宽 → 8 字节溢出改相邻 sds 头 → 64KB OOB
- broker 槽位 UAF + tcache 投毒到槽位数组；篡改 `jmp_buf` 校验与 RIP 后 `longjmp` 进 relay
- 之后走 ledger/council 门禁读 flag fd（broker 直接 open flag 因 namespace/权限失败）

## 解题思路

1. 堆 grooming：`PUT/SET/DEL/RESTORE` 让溢出落在 sds 头，放大读写窗口，改模块记录 `fptr` 为 relay。
2. broker：UAF 泄露与 safe-linking 投毒，伪造槽位读 GOT 得 libc，改 `setjmp` 保存区跳到 `sub_145A`。
3. 传输层对接已有 `ledger_lib` / `council_poc`，注意 council seq 从 2 起。

## 关键代码/payload

```text
# 高层: sds OOB → 改 fptr=relay → broker longjmp → ledger 0x60 → council gate → read fd4
```

## 参考链接

- https://xz.aliyun.com/news/93035
