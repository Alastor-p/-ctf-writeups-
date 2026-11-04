---
title: shell
competition: 羊城杯
year: 2026
category: Pwn
tags: ['stack-overflow', 'seccomp', 'orw', 'leave-ret', 'got']
sources: ['https://xz.aliyun.com/news/93035', 'https://xz.aliyun.com/news/93039']
---

# shell

## 题目信息

- 分类：PWN
- 保护：Partial RELRO，无 canary，NX，无 PIE
- seccomp：禁止 `execve` / `execveat`，其余放行 → 走 ORW
- 公开 WP 样例 flag：`DASCTF{9047…}`（动态容器值因实例而异）

## 考点

- `read(0, buf, 0x30)` 对 0x20 栈缓冲溢出，刚好控 saved rbp + rip
- `leave; ret` + 回跳 vuln 内 `lea rax,[rbp-0x20]; call read` → 任意地址写原语
- Partial RELRO：改 GOT；seccomp 下用 open/read/write

## 解题思路

1. 溢出把 rbp 指到可控区，rip 指回 `0x40122b`，串多轮「任意写 0x30」。
2. 把 `read@got` 临时改成写 gadget 泄露 libc；再用 PLT resolve 恢复 `read@got`。
3. 分块在 `.bss` 拼 ROP，最后 `pop rsp` 迁到大缓冲，ORW 读 flag。
4. 注意 resolver 的大栈需求（bss 高址）以及 `open` 后 rdx 被破坏需重设。

## 关键代码/payload

```text
# 每轮: rbp=A, rip=0x40122b → read(0, A-0x20, 0x30)
# 泄露后 ORW: open → read(fd,buf,n) → write(1,buf,n)
```

完整 exp 见先知原文，本仓库不复制完整 exploit。

## 参考链接

- https://xz.aliyun.com/news/93035
- https://xz.aliyun.com/news/93039
