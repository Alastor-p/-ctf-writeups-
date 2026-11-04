---
title: justledger
competition: 羊城杯
year: 2026
category: Pwn
tags: ['sqlite-extension', 'multi-process', 'uaf', 'fmtstr', 'stack-overflow']
sources: ['https://xz.aliyun.com/news/93035', 'https://xz.aliyun.com/news/93039']
---

# justledger

## 题目信息

- 分类：PWN（多进程账本链）
- 结构：`listener → justledger(+ledgerprobe.so) → ledgerbroker → ledgervault → flag`
- SQL authorizer 仅放行 SELECT/READ；flag 只在 vault 侧

## 考点

- SQLite 扩展对象 freelist / 任意写 → 劫持闲置 poll 转发到 broker
- broker window 长度检查只比低字节 → 越界读写相邻 ROUTE 对象
- vault：格式化串泄露 + 长度低字节绕过栈溢出 → ROP 读已打开 flag fd

## 解题思路

1. **probe**：`ledger_seed/bind` 武装后，`make/drop/touch` 污染释放链表，任意写覆盖 `ledger_fire` 指针到扩展内转发函数，把 TCP 接到 broker。
2. **broker**：越界读泄露 secret/基址，伪造 ROUTE3 编码指针，再跳到 broker 转发函数接到 vault。
3. **vault**：`0x91` 泄露 secret/canary/PIE/libc/flag_fd；`0xa7` 栈溢出后 ROP `read(flag_fd)` + `write(1)`。
4. 三层均不能直接读 flag，必须用两道「未使用转发函数」当跳板。

## 关键代码/payload

```sql
SELECT * FROM ledger WHERE seal=ledger_seed();
SELECT ledger_bind(ledger_seed(),0);
-- 其后 make/drop/touch/fire 打穿第一层（细节见原文）
```

PWN 完整协议帧与 ROP 见原文；此处仅保留链路级摘要。

## 参考链接

- https://xz.aliyun.com/news/93035
- https://xz.aliyun.com/news/93039
