# CISCN 2025（第十九届）暨第三届长城杯 · 初赛

路径：`writeups/ciscn/2025/`。各题摘要已加上 YAML frontmatter（`title`、`competition`、`year`、`category`、`tags`、`sources`），正文小节保持原样。下表相对链接仍指向同目录中的题目文件。

## 赛事概览

| 项目 | 内容 |
|------|------|
| 全称 | 第十九届全国大学生信息安全竞赛（创新实践能力赛）暨第三届「长城杯」网数智安全大赛（防护赛） |
| 初赛 | 2025-12-28 09:00–17:00（线上）；12-27 14:00 起可登录测试 |
| 主办 | 中国信息安全测评中心等（中央网信办、教育部等指导） |
| 官网 | [http://www.ciscn.cn/](http://www.ciscn.cn/) |
| 参赛手册 | [http://www.ciscn.cn/announcement/view/397](http://www.ciscn.cn/announcement/view/397) |
| 平台 | match.ichunqiu.com（赛时） |

## 题目索引（初赛，基于公开 WP）

| 题目 | 分类 | 关键技术/考点 | Writeup |
|------|------|----------------|---------|
| HelloGate / hellogate | Web | 图片尾部 PHP 源码；反序列化链读文件 | [摘要](web/hellogate.md) |
| AI_WAF | Web | MySQL 内联注释 / 关键词绕过 WAF + 联合注入 | [摘要](web/ai-waf.md) |
| EzJava | Web | Thymeleaf SSTI；过滤 `T()`/`new` 后用反射读文件 | [摘要](web/ezjava.md) |
| dedecms | Web | 弱口令进织梦后台 + 上传 | [摘要](web/dedecms.md) |
| redjs | Web | Next.js 相关 CVE（CVE-2025-55182） | [摘要](web/redjs.md) |
| babygame | Reverse | Godot 解包；运行时改 AES key | [摘要](reverse/babygame.md) |
| wasm-login | Reverse | WASM 登录；爆破毫秒时间戳使 MD5(check) 前缀命中 | [摘要](reverse/wasm-login.md) |
| EzFlag | Crypto/RE | 斐波那契模 16（Pisano 周期 24）生成 flag 字符 | [摘要](crypto/ezflag.md) |
| ECDSA | Crypto | 私钥由固定欢迎语 SHA512 派生，可直接重算 | [摘要](crypto/ecdsa.md) |
| RSA_NestingDoll | Crypto | Pollard p-1 分解嵌套模数 | [摘要](crypto/rsa-nestingdoll.md) |
| SnakeBackdoor 1–6 | Misc | 流量分析：爆破密码 → SSTI → RC4/SM4 后门 | [摘要](misc/snakebackdoor.md) |
| Eternum | Misc | 自定义帧 + AES-GCM C2；base32 藏 flag | [摘要](misc/eternum.md) |
| Ram_snoop | Pwn | Kernel module 任意读扫描用户态/内核中的 flag | [摘要](pwn/ram-snoop.md) |
| vvvmmm 等 | — | 部分战队提到未出/无完整公开 WP | 暂无公开 WP |

## 主要公开来源

- 千夏: https://l0serqianxia.github.io/blog/2025/12/29/ciscn-2025-personal-writeup/
- Yp0int: https://godownio.github.io/2025/12/20/2025-ciscn-chu-sai-wp-by-yp0int/
- luo-kaihong: https://luo-kaihong.github.io/p/2025-ciscn%E5%88%9D%E8%B5%9B/
- moyuin: https://moyuin.top/blog/%E9%95%BF%E5%9F%8E%E6%9D%AF%20WriteUP
- 52pojie: https://www.52pojie.cn/forum.php?mod=viewthread&tid=2083027
