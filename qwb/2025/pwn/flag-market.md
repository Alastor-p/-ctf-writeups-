# flag-market

## 题目信息
- 赛事：强网杯 2025 初赛
- 分类：Pwn

## 考点
- 读 flag 到栈但遇 `{` 截断打印
- BSS 上 `scanf("%s")` 溢出改 printf 格式串
- 格式化字符串改 GOT

## 解题思路
1. 程序打开 flag 读到栈上，打印时遇 `{` 停止；另有 BSS 溢出可覆盖 printf 用的格式串。
2. 第一次用格式串把 `exit`/`fclose` 一类 GOT 改回 `main`，并泄露 libc/栈。
3. 第二次把 `printf` GOT 改成 `system`，再传入 `/bin/sh` 拿壳。

## 关键代码/payload
```python
# 思路级伪代码：溢出入参覆盖 printf 格式 → %n 写 GOT
# 详见 W&M / SAINTSEC 原文完整 exp
```

## 参考链接
- https://blog.wm-team.cn/index.php/archives/87/
- https://cn-sec.com/archives/4597169.html

> 本文为对公开 writeup 的归纳总结，版权归原作者所有；请务必阅读原文核对细节。
