---
title: reverse02
competition: 网鼎杯
year: 2024
category: Reverse
tags: [白虎, rust, path-traversal]
sources:
  - https://mp.weixin.qq.com/s/5Xet54leUqVOeMYzTX0ROw
  - https://sechub.in/view/2964737
  - https://github.com/CTF-Archives/2024-wdb-baihu
---

# reverse02

## 题目信息

- 赛事：第四届网鼎杯 2024 线上资格赛 · 白虎组
- 分类：Reverse
- 题面：Rust 程序，听 8080，只处理 GET。题单见 [CTF-Archives](https://github.com/CTF-Archives/2024-wdb-baihu)。

## 考点

- 路径过滤只替换一次 `../`
- 用 `....//` 在替换后仍留下 `../`

## 解题思路

公开 WP 很短：服务把请求路径里的 `../` 换成 `/`。`....//` 被替换掉中间的 `../` 之后还剩 `../`，从而读到目标文件。没有更复杂的鉴权描述。

## 关键代码/payload

```text
GET ....//....//<目标路径>
# "../" → "/" 之后，"....//" 变成 "../"
```

## 参考链接

- https://sechub.in/view/2964737
- https://github.com/CTF-Archives/2024-wdb-baihu

> 本文为对公开 writeup 的归纳总结，版权归原作者所有；请务必阅读原文核对细节。
