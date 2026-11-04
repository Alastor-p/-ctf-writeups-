# 第十届强网杯 2026 线上赛 Writeup 摘要

路径：`writeups/qwb/2026/`。各题摘要已有 YAML frontmatter（`title`、`competition`、`year`、`category`、`tags`、`sources`），正文小节保持原样。下表相对链接仍指向同目录中的题目文件。

> 仅整理 **线上 Jeopardy**（约 2026-10-31～2026-11-01）。线下决赛（11-28～11-29）不在本目录范围。

## 赛事概览

| 项 | 内容 |
|---|---|
| 赛事 | 第十届“强网杯”全国网络安全挑战赛 · 线上赛 |
| 时间 | 2026-10-31 ～ 2026-11-01（Asia/Shanghai） |
| 规模 | 约 3206 支战队、14196 人报名；41 题，40 题被解出 |
| 题型分布 | Misc 6 · Crypto 6 · Reverse 3 · PWN 17 · Web 9 |
| 晋级 | 线上排名取 32 队进线下（郑州） |
| 官方 | [https://qiangwangbei.com/](https://qiangwangbei.com/) |
| 题包归档 | [https://github.com/CTF-Archives/2026-qwbs10-quals](https://github.com/CTF-Archives/2026-qwbs10-quals) |
| 收官报道 | [https://feng.ifeng.com/c/8xjEiguoKxk](https://feng.ifeng.com/c/8xjEiguoKxk) |

说明：摘要用中文转述公开 WP，并给出源链接；**不编造**未公开的 flag/手法。PWN 仅保留高阶思路，完整 PoC 请看原作者文章。动态容器 flag 在公开文中多为脱敏占位。

## 题目索引

| 分类 | 题目 | 摘要状态 |
|---|---|---|
| Misc | [宇宙微波背景辐射](misc/cmb-radiation.md) | 有摘要 |
| Misc | [0perator](misc/0perator.md) | 有摘要 |
| Misc | [NeuronShuffle](misc/neuron-shuffle.md) | 有摘要 |
| Misc | [谍影重重7](misc/bourne-ultimatum-7.md) | 有摘要 |
| Misc | [Dreambound](misc/dreambound.md) | 有摘要 |
| Misc | [问卷调查](misc/survey.md) | 有摘要 |
| Crypto | [frozen](crypto/frozen.md) | 有摘要 |
| Crypto | [vmshare](crypto/vmshare.md) | 有摘要 |
| Crypto | [hoRRibleRing](crypto/horrible-ring.md) | 有摘要 |
| Crypto | [zkRSA](crypto/zkrsa.md) | 有摘要 |
| Crypto | [crp-12025](crypto/crp-12025.md) | 有摘要 |
| Crypto | crp-11741 | 暂无公开WP |
| Reverse | [ELFStudy](reverse/elfstudy.md) | 有摘要 |
| Reverse | [firmware](reverse/firmware.md) | 有摘要 |
| Reverse | [license](reverse/license.md) | 有摘要 |
| Web | BlindReview | 暂无公开WP |
| Web | [cwp](web/cwp.md) | 有摘要 |
| Web | [ezphp](web/ezphp.md) | 有摘要 |
| Web | [ezstar](web/ezstar.md) | 有摘要 |
| Web | [ezcms](web/ezcms.md) | 有摘要 |
| Web | [Crack a Little Smile](web/crack-a-little-smile.md) | 有摘要 |
| Web | [fault_web_and_fault_hash](web/fault-web-and-fault-hash.md) | 有摘要 |
| Web | [vaultlink](web/vaultlink.md) | 有摘要 |
| Web | [vaultlink_revenge](web/vaultlink-revenge.md) | 有摘要 |
| Pwn | [babel](pwn/babel.md) | 有摘要 |
| Pwn | [babyark](pwn/babyark.md) | 有摘要 |
| Pwn | [babysilent](pwn/babysilent.md) | 有摘要 |
| Pwn | [babystar](pwn/babystar.md) | 有摘要 |
| Pwn | [Babyv8](pwn/babyv8.md) | 有摘要 |
| Pwn | [bad_puppet](pwn/bad-puppet.md) | 有摘要 |
| Pwn | [Blackout](pwn/blackout.md) | 有摘要 |
| Pwn | [drywell](pwn/drywell.md) | 有摘要 |
| Pwn | [easytl](pwn/easytl.md) | 有摘要 |
| Pwn | [HESEUS](pwn/heseus.md) | 有摘要 |
| Pwn | [oldsvr](pwn/oldsvr.md) | 有摘要 |
| Pwn | [ez_qemu](pwn/ez-qemu.md) | 有摘要 |
| Pwn | [CanonicoPWN](pwn/canonicopwn.md) | 有摘要 |
| Pwn | [hexachord](pwn/hexachord.md) | 有摘要 |
| Pwn | [What The Fox!](pwn/what-the-fox.md) | 有摘要 |
| Pwn | [shadowledger](pwn/shadowledger.md) | 有摘要 |
| Pwn | [Ironclad](pwn/ironclad.md) | 有摘要 |

### 暂无公开完整 WP / 未收录摘要

| 题目 | 说明 |
|---|---|
| BlindReview | 赛榜约 12 队解出；星宇Sec Web&Reverse 合集从 cwp 起篇，未见 BlindReview 专章 |
| crp-11741 | 赛榜 **0 队**解出；xiaoshabi 仓库有 FPGA→A5/1 流水线交接文档，但无完整公开 flag 题解 |

## 主要公开来源

1. https://eryuemu.com/blog/qwb-2026-neuron-shuffle-license-recap/ — NeuronShuffle、license  
2. https://github.com/xiaoshabi-cmd/qiangwangbei2026 — frozen、vmshare（及 crp-11741/hoRRibleRing 材料）  
3. https://blog.h-acker.cn/5688.html — PWN 17 题合集（转载微信公众号「星宇Sec」）  
4. https://cn-sec.com/archives/5548848.html — Web&Reverse 合集（CN-SEC）  
5. https://cn-sec.com/archives/5548779.html — Misc&Crypto 合集（CN-SEC）  
6. https://github.com/CTF-Archives/2026-qwbs10-quals — 题目列表与附件  

## 统计

- 本目录含完整中文摘要的题目数：**39**
- 索引中标记暂无公开 WP：**2**（BlindReview、crp-11741）
- 线上赛题目总数（官方/报道）：**41**
