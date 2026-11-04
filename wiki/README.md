# CTF-Wiki 中文文档（本地镜像）

本目录是 [CTF-Wiki](https://github.com/ctf-wiki/ctf-wiki) **简体中文文档**的摘录镜像，供本地阅读和检索增强（RAG）使用。正文版权归 CTF-Wiki 贡献者，许可为 **[CC BY-NC-SA 4.0](https://creativecommons.org/licenses/by-nc-sa/4.0/)**。完整许可证文本见同目录 [`LICENSE`](LICENSE)。署名与修改说明见仓库根目录 [`NOTICE.md`](../NOTICE.md)。

- 上游仓库：<https://github.com/ctf-wiki/ctf-wiki>
- 上游提交：[`e225ddfcd420a7f54a5940f47336ebdf8c29b875`](https://github.com/ctf-wiki/ctf-wiki/commit/e225ddfcd420a7f54a5940f47336ebdf8c29b875)（2026-08-23）
- 在线站点：<https://ctf-wiki.org>
- 上游路径：`docs/zh/docs/**` → 本目录去掉该前缀。例如上游 `docs/zh/docs/web/sqli.md` 对应 `wiki/web/sqli.md`。

## 收录范围

只收录中文 Markdown，以及两处页面直接引用、体积很小的矢量图 / 脚本：

- `pwn/linux/kernel-mode/figure/Kernel_Layout.svg`
- `crypto/blockcipher/figure/simon_key_schedule.svg`
- `crypto/signature/service.py`

未收录英文、繁体目录，也未收录 MkDocs 站点外壳（`docs/zh/docs/static/` 下的 css/js/logo）、Docker 与构建脚本。图片、GIF、Visio、压缩包等二进制约 582 个文件、70 MiB，为控制仓库体积已省略；文中相对图片路径仍按原样保留，对应文件在上游同一相对路径下。需要配图时，把 `wiki/<相对路径>` 换成：

```text
https://github.com/ctf-wiki/ctf-wiki/raw/e225ddfcd420a7f54a5940f47336ebdf8c29b875/docs/zh/docs/<相对路径>
```

目录内相对链接保持原有层级，因此章节之间的 `.md` 链接仍然指向本树。`reverse/platform/windows/unpack/unpack-dll.md` 里原先指向旧站点的绝对路径已改成同目录的 `./manually-fix-iat.md`。

## 姊妹项目（不入库）

CTF-Wiki 还有两个独立仓库，这里只作外部参考，不把它们的题目附件或工具说明搬进来：

- 题目与附件：[ctf-challenges](https://github.com/ctf-wiki/ctf-challenges)
- 工具说明：[ctf-tools](https://github.com/ctf-wiki/ctf-tools)

## 章节

| 目录 | 页面数 | 内容 |
|------|--------|------|
| [introduction](introduction/) | 6 | 入门、学习路线与资源 |
| [web](web/) | 6 | Web |
| [pwn](pwn/) | 151 | 二进制漏洞利用 |
| [crypto](crypto/) | 65 | 密码学 |
| [reverse](reverse/) | 48 | 逆向 |
| [misc](misc/) | 28 | 杂项 |
| [android](android/) | 16 | Android |
| [blockchain](blockchain/) | 22 | 区块链 |
| [ai](ai/) | 27 | AI / ML |
| [ics](ics/) | 4 | 工控 |
| [assembly](assembly/) | 4 | 汇编 |
| [executable](executable/) | 16 | ELF / PE 等可执行文件格式 |
| [contribute](contribute/) | 4 | 上游贡献与翻译说明 |
| 根目录 `index.md` / `usage.md` / `discussion.md` | 3 | 简介、使用方式、讨论 |

共 400 篇 Markdown。上游导航在 MkDocs 配置里，不在这些文件中；本地检索时直接按目录和正文搜索即可。

给新增或改写的百科页可选的 frontmatter 见 [`../templates/wiki-page.md`](../templates/wiki-page.md)。已镜像的上游页面保持原样，没有批量插入 frontmatter。
