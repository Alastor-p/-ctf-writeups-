# 第四届网鼎杯 2024 线上资格赛 Writeup 摘要

路径：`writeups/wdb/2024/`。只整理 **线上官方资格赛**（青龙 / 白虎 / 朱雀 / 玄武四场）。半决赛专项赛与安全运营赛不在本目录。

## 目录方案

四组题目并不共用同一套附件，因此按 **组别分子目录**（不是按分类平铺）：

```text
writeups/wdb/2024/<qinglong|baihu|zhuque|xuanwu>/<category>/<challenge>.md
```

组别目录：`qinglong` 青龙、`baihu` 白虎、`zhuque` 朱雀、`xuanwu` 玄武。分类目录仍是 `web`、`pwn`、`crypto`、`reverse`、`misc`。每篇 frontmatter 的 `tags` 里也写了组别，方便按标签过滤。

题号沿用公开文章和 [CTF-Archives](https://github.com/CTF-Archives) 的 `crypto01` / `pwn02` 这类名字。玄武组公开文里的 `crypto001`、`pwn3` 保留这个叫法。同一题名出现在不同组时内容不同，文件分开，不合并。

## 赛事概览

| 项 | 内容 |
|---|---|
| 赛事 | 第四届「网鼎杯」网络安全大赛 · 线上资格赛 |
| 时间 | 2024-10 下旬至 2024-11-04（四场错开） |
| 组别 | 青龙（高校等）、白虎（通信 / 交通 / 金融等）、朱雀（能源电力等）、玄武（科研 / 企业等） |
| 题单归档 | [青龙](https://github.com/CTF-Archives/2024-wdb-qinglong)、[白虎](https://github.com/CTF-Archives/2024-wdb-baihu)、[朱雀](https://github.com/CTF-Archives/2024-wdb-zhuque) |
| 玄武题单 | 未找到对等的 CTF-Archives 仓库。下表只列公开 WP 里出现过的题目，不补未出现的题号 |

说明：摘要用中文转述公开 WP，并给出源链接。**不编造**未公开的 flag 或手法。关键代码只留短片段，完整 exploit 看原文。不同文章给出的静态 flag 或口令若不一致，摘要里不收成唯一答案。

青龙组 CTF-Archives README 没有 Web 题，但多篇明确署名青龙的 WP 写了 web01、web02，因此仍收录。朱雀组归档里 Web-01、Pwn-01 的题面写成 `None`，其中 Web-01 仍有独立公开 WP。

## 青龙组

| 分类 | 题目 | 摘要状态 |
|---|---|---|
| Web | [web01](qinglong/web/web01.md) | 有摘要 |
| Web | [web02](qinglong/web/web02.md) | 有摘要 |
| Pwn | [pwn02](qinglong/pwn/pwn02.md) | 有摘要 |
| Pwn | pwn04 | 暂无公开 WP |
| Crypto | [crypto01](qinglong/crypto/crypto01.md) | 有摘要 |
| Crypto | [crypto02](qinglong/crypto/crypto02.md) | 有摘要 |
| Reverse | [reverse01](qinglong/reverse/reverse01.md) | 有摘要 |
| Reverse | [reverse02](qinglong/reverse/reverse02.md) | 有摘要 |
| Misc | [misc01](qinglong/misc/misc01.md) | 有摘要 |
| Misc | [misc02](qinglong/misc/misc02.md) | 有摘要 |
| Misc | [misc03](qinglong/misc/misc03.md) | 有摘要 |
| Misc | [misc04](qinglong/misc/misc04.md) | 有摘要 |

另有公开转载提到一场「知识竞赛签到，答对 8 题」。没有题目过程，不单独立篇。

## 白虎组

| 分类 | 题目 | 摘要状态 |
|---|---|---|
| Web | web01 | 暂无公开 WP |
| Pwn | [pwn01](baihu/pwn/pwn01.md) | 有摘要 |
| Pwn | pwn02 | 暂无公开 WP |
| Crypto | [crypto01](baihu/crypto/crypto01.md) | 有摘要 |
| Crypto | [crypto02](baihu/crypto/crypto02.md) | 有摘要 |
| Reverse | [reverse01](baihu/reverse/reverse01.md) | 有摘要 |
| Reverse | [reverse02](baihu/reverse/reverse02.md) | 有摘要 |
| Misc | [misc01](baihu/misc/misc01.md) | 有摘要 |
| Misc | [misc02](baihu/misc/misc02.md) | 有摘要 |
| Misc | [misc03](baihu/misc/misc03.md) | 有摘要 |
| Misc | [misc04](baihu/misc/misc04.md) | 有摘要 |

## 朱雀组

| 分类 | 题目 | 摘要状态 |
|---|---|---|
| Web | [web01](zhuque/web/web01.md) | 有摘要 |
| Pwn | pwn01 | 归档题面为 None，无公开 WP |
| Pwn | pwn02 | 暂无公开 WP |
| Crypto | crypto01 | 暂无公开 WP |
| Crypto | [crypto02](zhuque/crypto/crypto02.md) | 有摘要 |
| Crypto | [crypto03](zhuque/crypto/crypto03.md) | 有摘要 |
| Reverse | [reverse01](zhuque/reverse/reverse01.md) | 有摘要 |
| Reverse | [reverse02](zhuque/reverse/reverse02.md) | 有摘要 |
| Misc | [misc01](zhuque/misc/misc01.md) | 有摘要 |
| Misc | [misc02](zhuque/misc/misc02.md) | 有摘要 |
| Misc | [misc03](zhuque/misc/misc03.md) | 有摘要 |

## 玄武组

未见完整官方题单。下表只覆盖已读到的公开 WP。

| 分类 | 题目 | 摘要状态 |
|---|---|---|
| Web | [web01](xuanwu/web/web01.md) | 有摘要 |
| Web | [web03](xuanwu/web/web03.md) | 有摘要 |
| Pwn | [pwn02](xuanwu/pwn/pwn02.md) | 有摘要 |
| Pwn | [pwn03](xuanwu/pwn/pwn03.md) | 有摘要 |
| Crypto | [crypto001](xuanwu/crypto/crypto001.md) | 有摘要 |
| Reverse | [reverse02](xuanwu/reverse/reverse02.md) | 有摘要 |
| Misc | [misc01](xuanwu/misc/misc01.md) | 有摘要 |
| Misc | [misc02](xuanwu/misc/misc02.md) | 有摘要 |

若还存在 web02、pwn01、re01 等题号，目前没有可靠公开全文，表中不单列，避免把没见过的题写成「暂无 WP」。

## 主要公开来源

1. 青龙：ZeroPointZero（微信，CN-SEC 镜像）、ChaMd5、k1te、CTF-Archives 青龙题单  
2. 白虎：ChaMd5、Van1sh（青龙&白虎 crypto）、CTF-Archives 白虎题单  
3. 朱雀：ChaMd5、Van1sh、huggy、Carl Zhang、CTF-Archives 朱雀题单  
4. 玄武：ChaMd5、1cePeak、Van1sh、星盟 Polaris、看雪 / CTF 导航  

各题 `sources` 里是原文链接。微信原文打不开时，摘要依据可读镜像，sources 仍保留已知的 `mp.weixin.qq.com` 地址。

## 统计

- 本目录含中文摘要：**36**
- 题单里能对上、但没有可靠完整 WP：**6**（青龙 pwn04；白虎 web01、pwn02；朱雀 crypto01、pwn01、pwn02）
- 玄武组没有对等题单，未把「没见过的题号」算进缺口
