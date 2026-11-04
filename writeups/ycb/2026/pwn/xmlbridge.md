---
title: xmlbridge
competition: 羊城杯
year: 2026
category: Pwn
tags: ['libxml2', 'uaf', 'dict-oob', 'multi-hop', 'tcache']
sources: ['https://xz.aliyun.com/news/93035', 'https://xz.aliyun.com/news/93039']
---

# xmlbridge

## 题目信息

- 分类：PWN（五级服务链）
- 链：`xmlbridge → broker → manifestvault → keeper → oracle(flag)`
- 前端：1B opcode + 4B BE len；后端：2B BE len；`D` 操作做隧道

## 考点

- libxml2：`xmlDict` 表与网关缓冲相邻；DTD 错误回调把 `dict->size` 128→129，hash 命中 128 槽越界写 `valid=1` 过网关
- 后续各跳：任意相对读、无 canary 栈溢出、tcache 投毒、格式化串、有符号 VM 寄存器

## 解题思路

1. 按固定 L/I/R/C/S/E 布局堆，使 dict 结构复用已释放 0x500 块；A 段 DTD+未声明元素+大量新名字爆破过 `B`/`D` 网关。
2. `D` 隧道内跑 broker（收据 UAF/VIEW 泄露/COMMIT 溢出）→ manifest（GLANCE+CORRECT 投毒）→ keeper（fmt+溢出）→ oracle（改寄存器调读 flag）。
3. dict seed 每进程随机，需多连接重试网关。

## 关键代码/payload

```xml
<!DOCTYPE root [<!ELEMENT root ANY>]>
<root><zzz/><n0000/>...<n0119/></root>
```

（语言：用于触发 DTD 未知元素并把 dict size 推到 129；完整五跳脚本见原文。）

## 参考链接

- https://xz.aliyun.com/news/93035
- https://xz.aliyun.com/news/93039
