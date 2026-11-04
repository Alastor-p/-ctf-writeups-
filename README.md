# CTF 知识库

给本地模型和检索增强（RAG）用的 CTF 资料库。材料分成两套，不要混成一种许可：

- [`wiki/`](wiki/)：概念和知识。来自 [CTF-Wiki](https://github.com/ctf-wiki/ctf-wiki) 简体中文文档，**CC BY-NC-SA 4.0**。
- [`writeups/`](writeups/)：赛事题目的原创摘要。每题保留原文链接，技术段落不整篇照搬。

在线阅读上游百科仍以 <https://ctf-wiki.org> 为准。本仓库把中文 Markdown 放到本地，方便离线切块、嵌入和按目录过滤。

## 目录

```
/
├── README.md                 # 本文件
├── LICENSE                   # 仓库许可：wiki/ 与 writeups/ 分开
├── NOTICE.md                 # CTF-Wiki 署名与本次修改说明
├── wiki/                     # CTF-Wiki 中文文档
│   ├── LICENSE               # CC BY-NC-SA 4.0 全文
│   ├── README.md
│   └── <topic>/...           # introduction, web, pwn, crypto, reverse, misc,
│                             # android, blockchain, ai, ics, assembly,
│                             # executable, contribute
├── writeups/                 # 赛题摘要
│   └── <competition>/<year>/<category>/<challenge>.md
└── templates/
    ├── writeup.md            # 赛题摘要模板
    └── wiki-page.md          # 百科页可选 frontmatter
```

## 两套语料

| 目录 | 用途 | 适合的问题 |
|------|------|------------|
| `wiki/` | 方向综述、原理、常见手法 | 「SROP 是什么」「tcache 攻击有哪些」 |
| `writeups/` | 某场比赛某题的短摘要 | 「强网杯 2025 ezphp 怎么做」 |

赛题摘要目前包括：

| 赛事 | 年份 | 目录 |
|------|------|------|
| 强网杯（第九届） | 2025 | [writeups/qwb/2025](writeups/qwb/2025/) |
| 全国大学生信息安全竞赛 CISCN（第十九届，暨第三届长城杯） | 2025 | [writeups/ciscn/2025](writeups/ciscn/2025/) |
| DEF CON CTF Qualifier | 2025 | [writeups/defcon-quals/2025](writeups/defcon-quals/2025/) |

单题文件的 frontmatter：

```yaml
title: 题目名
competition: 强网杯
year: 2025
category: Web          # Web | Pwn | Crypto | Reverse | Misc | ...
tags: [考点短标签]
sources: [https://example.com/original-writeup]
```

正文固定为「题目信息 / 考点 / 解题思路 / 关键代码/payload / 参考链接」。新题照 [`templates/writeup.md`](templates/writeup.md) 写，并在该年 `README.md` 的索引表加一行。

## 本地检索怎么切

建议把下面两类 Markdown 都做嵌入，用 frontmatter 和路径过滤，而不是把整仓合成一个无差别索引：

- `wiki/**/*.md`
- `writeups/**/*.md`

实用做法：

1. 按文件切块。百科页长，按标题再切开；赛题摘要通常一整篇就是一块。
2. 元数据至少留下 `path`。赛题再写入 `competition`、`year`、`category`、`tags`、`sources`。
3. 问「某年某类比赛题」时，先限制 `path` 前缀为 `writeups/`，再用 `year` / `category` 过滤。问原理时限制为 `wiki/<topic>/`。
4. `wiki/` 里的图片大多没有放进仓库，相对路径仍然写着。块文本以 Markdown 正文为准；配图需要时按 [`NOTICE.md`](NOTICE.md) 的 raw 链接回上游取。
5. 回答时带上 `sources` 或百科页路径，方便核对。

`templates/`、本文件和 `NOTICE.md` 是说明，一般不必送进向量库。`wiki/LICENSE` 是法律文本，也不适合当知识块。

## 许可

- **`wiki/`**：CC BY-NC-SA 4.0。非商业、署名、相同方式共享。全文在 [`wiki/LICENSE`](wiki/LICENSE)，署名和省略了哪些附件见 [`NOTICE.md`](NOTICE.md)。不要把这套文档用于商业产品，也不要拿掉署名。
- **`writeups/`**：本仓库写的摘要。转载摘要时保留每篇的来源链接。链接指向的原文版权归原作者。

## 外部参考（不入库）

CTF-Wiki 的姊妹仓库只作链接，不把题目附件和工具手册复制进来：

- 知识：<https://github.com/ctf-wiki/ctf-wiki> ，站点 <https://ctf-wiki.org>
- 题目与附件：<https://github.com/ctf-wiki/ctf-challenges>
- 工具：<https://github.com/ctf-wiki/ctf-tools>

## 如何补充赛题

1. 新建 `writeups/<slug>/<year>/<category>/<challenge>.md`。
2. 用自己的话写考点和思路，关键代码只留短片段，完整 exploit 用链接指向原文。
3. 在该年 `README.md` 的题目表加一行。
4. 不编造未公开的题目、flag 或技术。没有公开题解就在表里写「暂无公开 WP」，不要造一篇摘要。
5. 中文优先。

分类目录：`web`、`pwn`、`crypto`、`reverse`、`misc`，以及以后可能出现的 `blockchain`、`ai`。

## 免责声明

内容仅供安全研究与学习。攻击手法的描述来自已公开资料，读者自行对使用行为负责。
