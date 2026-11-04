---
title: pwn03
competition: 网鼎杯
year: 2024
category: Pwn
tags: [玄武, kernel, uaf, pipe-buffer, msg-msg]
sources:
  - https://www.ctfiot.com/214152.html
  - https://sechub.in/view/2966475
  - http://sechub.in/view/2979334
---

# pwn03

## 题目信息

- 赛事：第四届网鼎杯 2024 线上资格赛 · 玄武组
- 分类：Pwn
- 公开文章写作 `pwn3`。设备节点 `/dev/easy`，`/proc/kallsyms` 可读。

## 考点

- 驱动里的 UAF（ioctl 分配 / 释放，read、write 仍可用）
- `msg_msg` 泄漏相邻对象
- 伪造 `pipe_buffer.ops`，把栈劫持到用户缓冲区上的 ROP
- `commit_creds(init_cred)` 提权

## 解题思路

ChaMd5 的公开分析：先从 kallsyms 读 `startup_64`，用固定偏移换出 `commit_creds` 和 `init_cred`。驱动提供 create / delete / read / write。在喷了一堆 `msg_msg` 的间隙里分配再释放驱动对象，读出来的是被消息复用后的内容，从而拿到堆上相邻 `msg_msg` 的指针。

改掉 `msg_msg` 的长度和指针后，用 `MSG_COPY` 再读一块，泄漏更远的地址。释放驱动对象、喷 `pipe`，让 `pipe_buffer` 占住同一块。把 `ops` 指到堆上的假表，表项是 `push rsi; pop rsp` 一类 gadget，关闭管道时内核顺着假 ops 把栈迁到这块缓冲区。缓冲区里是提权 ROP，最后回到用户态的 shell。

完整的消息队列布局和 gadget 偏移见原文，这里不复制那份内核 exp。

## 关键代码/payload

```text
kallsyms: startup_64 → commit_creds / init_cred
UAF 对象被 msg_msg 占住 → 泄漏堆
pipe_buffer.ops = 堆上的 pivot
ROP: pop rdi; init_cred; commit_creds; swapgs; iretq
```

## 参考链接

- https://www.ctfiot.com/214152.html
- https://sechub.in/view/2966475

> 本文为对公开 writeup 的归纳总结，版权归原作者所有；请务必阅读原文核对细节。
