# DEF CON CTF Qualifier 2025

路径：`writeups/defcon-quals/2025/`。各题摘要已加上 YAML frontmatter（`title`、`competition`、`year`、`category`、`tags`、`sources`），正文小节保持原样。下表相对链接仍指向同目录中的题目文件。

## 赛事概览

| 项目 | 内容 |
|------|------|
| 时间 | 2025-04-12 00:00 UTC — 2025-04-14 00:00 UTC |
| 形式 | 线上 Jeopardy |
| 出题 | Nautilus Institute |
| 官网 | https://nautilus.institute/ |
| CTFtime | [https://ctftime.org/event/2604/](https://ctftime.org/event/2604/) （本环境抓取返回 403，链接仍保留供读者访问） |
| 题目列表聚合 | [https://ctfpal.com/writeups/ctf/def-con-ctf-qualifier-2025-2604](https://ctfpal.com/writeups/ctf/def-con-ctf-qualifier-2025-2604) |
| **官方源码+solver** | [https://github.com/Nautilus-Institute/quals-2025](https://github.com/Nautilus-Institute/quals-2025) |

共约 44 题；官方在 GitHub 开源了资格赛题目与多数 solver。社区长文 WP 相对少，本批对有详细文章的 **rainbow mountain (rbm)**、**dialects** 做中文摘要，其余在表中指向官方仓库。

## 题目索引（节选）

| 题目 | 分类 | 关键技术/考点 | Writeup |
|------|------|----------------|---------|
| rainbow mountain (rbm) | Reverse | 静态链接 C++；函数表 + base64 输入；回文约束下的栈溢出改 target | [摘要](reverse/rainbow-mountain.md) |
| dialects | Crypto/Reverse | TLS+魔改 SM4-CTR / SM3；pow 式前缀零；读 flag 文件 | [摘要](crypto/dialects.md) |
| tenspades / seven_el_bee / holographic | — | 官方 solver 见仓库 | [官方](https://github.com/Nautilus-Institute/quals-2025) |
| jxl4fun | — | JPEG XL 相关；官方 solver | [官方](https://github.com/Nautilus-Institute/quals-2025) |
| callmerust | — | Rust；官方 solver | [官方](https://github.com/Nautilus-Institute/quals-2025) |
| memorybank / petshop / nfuncs / ywdap / im-pio-ssible | — | 官方 solver | [官方](https://github.com/Nautilus-Institute/quals-2025) |
| NautilusInstituteContinuousIntegrationAndContinuousDelivery | — | CI/CD 题；官方 solver | [官方](https://github.com/Nautilus-Institute/quals-2025) |
| 其余未开源社区长文的题 | — | 见 CTFtime tasks / CTF Pal | 暂无中文长文 WP（有官方代码） |

## 主要公开来源

- CTF-BR / Cloudlabs: https://blog.cloudlabs.ufscar.br/sec/defcon-quals-2025/
- Nautilus quals-2025: https://github.com/Nautilus-Institute/quals-2025
- CTF Pal 聚合: https://ctfpal.com/writeups/ctf/def-con-ctf-qualifier-2025-2604
