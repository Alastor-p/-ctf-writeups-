---
title: "Yamcs"
competition: "强网杯"
year: 2025
category: "Web"
tags:
  - "YAMCS 开源测控系统"
  - "Algorithms 中可配置/执行 Java 代码"
  - "报错带回显（环境不出网）"
sources:
  - "https://blog.wm-team.cn/index.php/archives/87/"
  - "https://cn-sec.com/archives/4597169.html"
---
# Yamcs

## 题目信息
- 赛事：强网杯 2025 初赛
- 分类：Web

## 考点
- YAMCS 开源测控系统
- Algorithms 中可配置/执行 Java 代码
- 报错带回显（环境不出网）

## 解题思路
1. 进入项目 Algorithms（如 `/myproject/copySunsensor`）发现可自定义算法逻辑。
2. 写入恶意 Java，利用异常信息或回显通道拿到命令执行/读文件结果。

## 关键代码/payload
原文未给出可摘录的短代码，请参阅参考链接中的完整 exploit。

## 参考链接
- https://blog.wm-team.cn/index.php/archives/87/
- https://cn-sec.com/archives/4597169.html

> 本文为对公开 writeup 的归纳总结，版权归原作者所有；请务必阅读原文核对细节。
