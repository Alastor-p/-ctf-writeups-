# 羊城杯 2026 初赛 Writeup 摘要

> 整理公开 WP 中可核对的初赛题（约 2026-10 下旬，DASCTF 平台）。不含强网杯。

## 赛事概览

| 项 | 内容 |
|---|---|
| 赛事 | 2026 年“羊城杯”网络安全大赛 · 初赛 |
| 时间 | 约 2026-10（Asia/Shanghai）；公开 WP 多见于 10-24～10-25 |
| 平台 | DASCTF（flag 形如 `DASCTF{...}`） |
| 题包归档 | [https://github.com/CTF-Archives/2026-YCB-Quals](https://github.com/CTF-Archives/2026-YCB-Quals)（镜像等以实际可达为准） |
| 主要 WP | 先知社区合集（自然 / bkbqwq） |

说明：摘要用中文转述公开 WP；**不编造**未公开内容。PWN 仅高阶思路，完整 PoC 见原文。

## 题目索引

| 分类 | 题目 | 摘要状态 |
|---|---|---|
| Pwn | [shell](pwn/shell.md) | 有摘要 |
| Pwn | [justledger](pwn/justledger.md) | 有摘要 |
| Pwn | [redisrelay](pwn/redisrelay.md) | 有摘要 |
| Pwn | [xmlbridge](pwn/xmlbridge.md) | 有摘要 |
| Pwn | [vaultcache](pwn/vaultcache.md) | 有摘要 |
| Pwn | cacheline / notebook / BabyMenu / LibraryManagementSystem | 暂无公开完整 WP（分析笔记未解出） |
| Pwn | [FedResNyFinLedgerOs](pwn/fedresnyfinledgeros.md) | 有摘要 |
| Reverse | [千千的咲](reverse/qianqian-de-xiao.md) | 有摘要 |
| Reverse | [VVMM](reverse/vvmm.md) | 有摘要 |
| Web | [DataPulse](web/datapulse.md) | 有摘要 |
| Web | [pdfchallenge](web/pdfchallenge.md) | 有摘要 |
| Web | [FluxPipe](web/fluxpipe.md) | 有摘要 |
| Web | [GraphNexus](web/graphnexus.md) | 有摘要 |
| Misc/AI 等 | NeuralVault、Chronos-Vault、Jammed、skin secret、谁教坏了我的Agent、Lost_Memory 等 | 题包有归档；本批未收录完整中文长文 WP |

## 主要公开来源

1. https://xz.aliyun.com/news/93035 — 羊城杯2026wp（自然）：PWN 合集 + DataPulse + 逆向
2. https://xz.aliyun.com/news/93039 — 羊城杯wp（bkbqwq）：Web 多题 + RE/PWN 赛后复盘
3. https://github.com/CTF-Archives/2026-YCB-Quals — 初赛题面/附件归档

## 统计

- 本目录含完整中文摘要：**12**
- 索引中标记暂无完整公开 WP / 未收录：**若干**（未解出 PWN、部分 Misc/AI）
