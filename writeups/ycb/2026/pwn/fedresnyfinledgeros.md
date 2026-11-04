---
title: FedResNyFinLedgerOs
competition: 羊城杯
year: 2026
category: Pwn
tags: ['vm-escape', 'yoloos', 'seccomp', 'aslr-bypass', 'rop']
sources: ['https://xz.aliyun.com/news/93039']
---

# FedResNyFinLedgerOs

## 题目信息

- 分类：PWN / 虚拟机逃逸
- 宿主：static-PIE x86-64，模拟 16 位 YOLOOS；seccomp 仅允许 read/write/open/close/exit
- 公开 WP 样例 flag：`DASCTF{7937…}`

## 考点

- guest 缓冲校验盲区 → 内核栈覆盖 → MMIO cache 写穿到宿主栈 saved RIP
- 指令上限 fault 写入与 PIE 相关的 poison，再 ENTERU 混合后可逆推基址
- 宿主 ROP：open/read/write 读 flag

## 解题思路

1. 客态 SYS_READ 向允许区间写大缓冲，覆盖内核返回槽并枢轴到 cache store 循环。
2. 写穿 ZCACHE 映射的宿主栈，覆盖 `main` saved RIP。
3. 先烧约 5e8 指令触发 limit，再 dump 混合结果反推 PIE；同进程第二阶段 ROP 读文件。

## 关键代码/payload

```text
# Stage1: burn instructions → poison
# Stage2: dump 0xe1e0 → invert mix → base
# Stage3: guest overwrite → host ROP open/read/write
```

完整汇编与 invert 见原文。

## 参考链接

- https://xz.aliyun.com/news/93039
