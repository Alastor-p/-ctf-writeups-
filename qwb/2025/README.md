# 强网杯 2025（第九届）

## 赛事概览

| 项目 | 内容 |
|------|------|
| 全称 | 第九届「强网杯」全国网络安全挑战赛 |
| 初赛 | 2025-10-18 00:00 — 2025-10-19 00:00（线上 Jeopardy） |
| 决赛 | 2025-11-22 — 11-23（线下，中国网络安全科技馆） |
| 指导 | 中央网信办、河南省人民政府 |
| 主办 | 河南省委网信办、河南省教育厅、郑州市人民政府、信息工程大学、郑州大学、中国网络空间安全协会等 |
| 平台 | [qiangwangbei.com](https://www.qiangwangbei.com/) / [i春秋赛页](https://www.ichunqiu.com/competition/detail/369) |
| CTFtime | 暂未在本批核验到稳定事件页（部分镜像站收录初赛 WP） |

本目录以**初赛**公开 writeup 为主；决赛 Realworld/AWDU 题因公开材料较少，仅在文末列表备注。

## 题目索引（初赛）

| 题目 | 分类 | 关键技术/考点 | Writeup |
|------|------|----------------|---------|
| SecretVault | Web | Go 前置鉴权 + Python 后端；`Connection` hop-by-hop 删头绕过 `X-User` | [摘要](web/secretvault.md) |
| ezphp | Web | PHP 反序列化 / 匿名类 + phar include 绕过 + SUID | [摘要](web/ezphp.md) |
| bbjv | Web | Spring SpEL 表达式注入，改 `user.home` | [摘要](web/bbjv.md) |
| Yamcs | Web | YAMCS 算法配置可执行 Java | [摘要](web/yamcs.md) |
| 日志系统 | Web | PHP 数组参数解析 + 路径拼接写 webshell；内网 JBoss RCE | [摘要](web/rizhi-xitong.md) |
| PTer | Web | BT Tracker SQL 注入（XFF 伪造 IP）+ 文件包含 | [摘要](web/pter.md) |
| flag-market | Pwn | BSS 溢出改 printf 格式串 → 改 GOT / system | [摘要](pwn/flag-market.md) |
| adventure | Pwn | 商店整数溢出；屠龙戒指 strcpy → House of Apple | [摘要](pwn/adventure.md) |
| Bph | Pwn | 大 size malloc 失败后任意偏移 null；stdin FSOP ORW | [摘要](pwn/bph.md) |
| sockserver | Pwn | SOCKS 代理式堆管理漏洞；伪造 link_map + ret2dl | [摘要](pwn/sockserver.md) |
| check-little | Crypto | RSA e=3，`gcd(c,N)` 分解 | [摘要](crypto/check-little.md) |
| butterfly / Buttferfly | Reverse | 硬编码密钥 `MMXEncod` 的 MMX 风格块解密 | [摘要](reverse/butterfly.md) |
| tradre | Reverse | 父子进程 ptrace 虚拟机；AES + 伪随机密钥派生 | [摘要](reverse/tradre.md) |
| Personal Vault | Misc | Windows 内存取证，搜索 `flag{` | [摘要](misc/personal-vault.md) |
| 谍影重重 6.0 | Misc | RTP/UDP 提音频 → 八进制密文 → 历史梗 md5 | [摘要](misc/dieying-chongchong.md) |
| legacyOLED | Misc | I2C / OLED 帧还原 + LSB 隐写 | [摘要](misc/legacy-oled.md) |
| The_Interrogation_Room | Misc | 线性方程组式「审讯」+ PoW | [摘要](misc/the-interrogation-room.md) |
| Qcalc | Misc | Android deeplink + SnakeYAML 反序列化 RCE | [摘要](misc/qcalc.md) |
| cpc | Misc | Check Point VPN 任意文件读（CVE-2024-24919）审计日志 | [摘要](misc/cpc.md) |
| 问卷调查 / 签到 | Misc | 填问卷 / 复制即可 | 见 [CN-SEC SAINTSEC 转载](https://cn-sec.com/archives/4592147.html) |

## 决赛公开题（简述，暂无独立摘要页）

| 题目 | 分类 | 备注 | 来源 |
|------|------|------|------|
| perpetual / TrustSQL / Forge | Realworld | Solana perpetuals 0day、TrustSQL、侧信道等 | [https://nvme0n1p.dev/posts/2025-qwb-final](https://nvme0n1p.dev/posts/2025-qwb-final) |
| fox / smiles | AWDU | 任意读、Zip 任意写；Pwn 后门 | 同上 |
| 其他决赛题 | — | 部分队博有写 | [https://jia.je/ctf-writeups/2025-11-22-qiangwangbei-final-2025/index.html](https://jia.je/ctf-writeups/2025-11-22-qiangwangbei-final-2025/index.html) |

## 主要公开来源

- W&M Team: https://blog.wm-team.cn/index.php/archives/87/
- SAINTSEC（CN-SEC 转载）: https://cn-sec.com/archives/4597169.html / https://cn-sec.com/archives/4592147.html
- nvme0n1p 决赛: https://nvme0n1p.dev/posts/2025-qwb-final
- jiegec / Redbud: https://jia.je/ctf-writeups/2025-11-22-qiangwangbei-final-2025/index.html
