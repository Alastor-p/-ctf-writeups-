---
title: "Ram_snoop"
competition: "全国大学生信息安全竞赛"
year: 2025
category: "Pwn"
tags:
  - "Linux kernel module `/dev/noc`"
  - "flag 被用户态进程读入内存后删文件"
  - "写爆 tail 解除读偏移限制后扫内存"
sources:
  - "https://moyuin.top/blog/%E9%95%BF%E5%9F%8E%E6%9D%AF%20WriteUP"
---
# Ram_snoop

## 题目信息
- 赛事：CISCN 2025 初赛
- 分类：Pwn

## 考点
- Linux kernel module `/dev/noc`
- flag 被用户态进程读入内存后删文件
- 写爆 tail 解除读偏移限制后扫内存

## 解题思路
1. 环境加载 `babydev.ko`；`eatFlag` 把 `/flag` 读进内存再删除。
2. ioctl 可泄露 `global_buf`；大量 write 推高 tail 后即可大范围 read。
3. 从偏移处暴力搜 `flag{` 字符串。

## 关键代码/payload
原文未给出可摘录的短代码，请参阅参考链接中的完整 exploit。

## 参考链接
- https://moyuin.top/blog/%E9%95%BF%E5%9F%8E%E6%9D%AF%20WriteUP

> 本文为对公开 writeup 的归纳总结，版权归原作者所有；请务必阅读原文核对细节。
