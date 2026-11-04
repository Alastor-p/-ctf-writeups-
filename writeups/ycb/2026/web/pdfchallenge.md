---
title: pdfchallenge
competition: 羊城杯
year: 2026
category: Web
tags: ['markdown', 'cherry', 'xss', 'file-protocol', 'pdf']
sources: ['https://xz.aliyun.com/news/93039']
---

# pdfchallenge

## 题目信息

- 分类：WEB
- 流程：提交 Markdown → Cherry 渲染 → 无头浏览器打印 PDF
- 渲染中间页为 `file:///tmp/renders/…`（file 源）

## 考点

- code fence 语言名拼进 `data-lang` 未转义；先渲染进缓存再 DOMPurify，缓存还原绕过清洗
- file 协议下 iframe 可读渲染进程本地文件，内容进 PDF

## 解题思路

1. 确认 `/render` 返回 PDF，中间页为 file://。
2. 语言名注入：`x"><iframe src=file:///flag …>`（注意 toLowerCase，路径小写）。
3. `pdftotext` 提取；多路径探测 `/flag` 等。
4. 赛后复盘指出不同 Cherry/模板 build 上注入是否生效有差异。

## 关键代码/payload

语言名注入（Markdown code fence 的 language 字段）：

```text
x"><iframe src=file:///flag width=800 height=600></iframe>
```

整段提交示意：开启 code fence，language 填上述字符串，正文随意。

## 参考链接

- https://xz.aliyun.com/news/93039
