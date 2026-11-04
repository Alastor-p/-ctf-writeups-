---
title: fault_web_and_fault_hash
competition: 强网杯
year: 2026
category: Web
tags: ['fault-injection', 'hash', 'web']
sources: ['https://cn-sec.com/archives/5548848.html', 'https://github.com/CTF-Archives/2026-qwbs10-quals']
---

# fault_web_and_fault_hash


## 题目信息

- 分类：Web
- 题面：everything it trusts stays in the dark.
- 多实例地址（注意勿多开排队）
- 公开解出：约 133 队

## 考点

- 故障注入 / 错误哈希校验逻辑
- 服务端信任边界

## 解题思路

公开 Web7：围绕“fault”与 hash 校验不一致或可诱导的错误路径，构造请求使服务在错误状态下给出敏感信息或越权结果。具体故障模型以源文实验为准。

## 关键代码/payload

见 https://cn-sec.com/archives/5548848.html。

## 参考链接

- https://cn-sec.com/archives/5548848.html
