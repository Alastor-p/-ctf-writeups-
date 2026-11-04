---
title: ELFStudy
competition: 强网杯
year: 2026
category: Reverse
tags: ['elf', 'crypto-rev', 'custom-cipher']
sources: ['https://cn-sec.com/archives/5548848.html', 'https://github.com/CTF-Archives/2026-qwbs10-quals']
---

# ELFStudy


## 题目信息

- 分类：Reverse
- 公开解出：约 1434 队（线上赛最快首解之一，开赛约 2 分 36 秒）
- 附件：见 CTF-Archives release

## 考点

- ELF 结构与校验逻辑逆向
- 自定义密钥扩展 / 加密轮函数还原

## 解题思路

公开 Web&Reverse 合集 Reverse1 章节：分析程序如何读取输入并与内置表/轮函数比较。WP 还原了密钥扩展与加密/校验循环（约 2..31 轮），据此写出解密脚本得到 flag。题目相对入门，故解出队伍最多。

## 关键代码/payload

见 https://cn-sec.com/archives/5548848.html Reverse1-ELFStudy（含密钥扩展伪代码）。

## 参考链接

- https://cn-sec.com/archives/5548848.html
- https://github.com/CTF-Archives/2026-qwbs10-quals
