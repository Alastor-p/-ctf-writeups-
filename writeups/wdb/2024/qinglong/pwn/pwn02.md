---
title: pwn02
competition: 网鼎杯
year: 2024
category: Pwn
tags: [青龙, stack-pivot, backdoor, i386]
sources:
  - https://mp.weixin.qq.com/s/HhL4lqcL_3EeYg1TDeBOKg
  - https://cn-sec.com/archives/3336366.html
  - https://sechub.in/view/2962999
  - https://www.cnblogs.com/backlion/p/18527653
  - https://github.com/CTF-Archives/2024-wdb-qinglong
---

# pwn02

## 题目信息

- 赛事：第四届网鼎杯 2024 线上资格赛 · 青龙组
- 分类：Pwn
- 题面：32 位服务。登录后进入漏洞函数。题单见 [CTF-Archives](https://github.com/CTF-Archives/2024-wdb-qinglong)。

## 考点

- 固定口令进入漏洞路径
- 溢出长度不够时做栈迁移
- 二进制里现成的 `system` 与 `/bin/sh`

## 解题思路

登录比较的是 `admin` / `admin123`，对上才能走到 `vuln`。程序会打印缓冲区地址。公开分析里能直接盖住的只有大约两个指针那么宽（有的文章写成 8 字节、有的按 0x50 的 payload 写），不够摆完整 ROP，所以把返回地址迁到这块已知栈上。

后门函数和 `/bin/sh` 字符串都在二进制里。栈迁移之后在泄漏地址处放 `system("/bin/sh")` 即可。各文的 gadget 地址不一致，以自己附件的 `leave; ret` 和后门为准。完整 exp 见原文，这里不收录。

## 关键代码/payload

```text
username admin / password admin123
泄漏 buf → payload 末尾覆盖为 buf-4 + leave_ret
栈上放置 system("/bin/sh")
```

## 参考链接

- https://cn-sec.com/archives/3336366.html
- https://sechub.in/view/2962999
- https://www.cnblogs.com/backlion/p/18527653

> 本文为对公开 writeup 的归纳总结，版权归原作者所有；请务必阅读原文核对细节。
