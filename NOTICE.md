# 声明与署名

## CTF-Wiki

`wiki/` 中的文档来自 CTF-Wiki 简体中文文档，并按 [CC BY-NC-SA 4.0](https://creativecommons.org/licenses/by-nc-sa/4.0/) 分享。

| 项 | 内容 |
|----|------|
| 作品 | CTF-Wiki |
| 上游仓库 | <https://github.com/ctf-wiki/ctf-wiki> |
| 在线版本 | <https://ctf-wiki.org> |
| 固定提交 | [`e225ddfcd420a7f54a5940f47336ebdf8c29b875`](https://github.com/ctf-wiki/ctf-wiki/commit/e225ddfcd420a7f54a5940f47336ebdf8c29b875)（2026-08-23） |
| 上游路径 | `docs/zh/docs/**` |
| 本仓库路径 | `wiki/**`（去掉 `docs/zh/docs/` 前缀） |
| 许可证全文 | [`wiki/LICENSE`](wiki/LICENSE) |
| 许可证说明 | <https://creativecommons.org/licenses/by-nc-sa/4.0/> |

使用或再分发 `wiki/` 时请保留本文件、`wiki/LICENSE` 与上述署名，并遵守非商业（NC）与相同方式共享（SA）。改编部分同样以 CC BY-NC-SA 4.0 发布。

## 相对上游的修改

这次导入是对上游文档集合的改编，改动如下：

1. **路径。** 只取出 `docs/zh/docs/**`，放到 `wiki/`。未导入英文 / 繁体树、MkDocs 配置、Docker、脚本，以及 `docs/zh/docs/static/` 下的站点样式与 logo。
2. **省略体积较大的二进制附件。** 未纳入图片与其它二进制共 582 个文件、73,227,120 字节（约 70 MiB），其中 PNG 521、JPG 50、GIF 5、JPEG 1、站点 logo PNG 1、VSDX 1、RAR 1，另有未使用的站点 `extra.js` / `extra.css`。Markdown 正文里的相对图片路径保持不变，便于以后按同一相对路径补回，或按下面的规则回源查看：

   ```text
   https://github.com/ctf-wiki/ctf-wiki/raw/e225ddfcd420a7f54a5940f47336ebdf8c29b875/docs/zh/docs/<wiki 内相对路径>
   ```

3. **保留的小文件。** 除 400 篇 Markdown 外，保留了页面直接引用的 `Kernel_Layout.svg`、`simon_key_schedule.svg` 和 `crypto/signature/service.py`。
4. **一处站内链接。** `wiki/reverse/platform/windows/unpack/unpack-dll.md` 中两处旧站点绝对路径 `/reverse/unpack/manually-fix-iat/index.html` 改为同目录相对链接 `./manually-fix-iat.md`。该文件顶部有修改注释。其余 Markdown 与上游该提交中的对应文件一致。
5. **本仓库新增、不属于上游正文的文件。** `wiki/README.md` 是镜像说明。它描述上述改编，随 `wiki/` 一并按 CC BY-NC-SA 4.0 提供。

## 本仓库其它内容

`writeups/` 是本仓库编写的赛题摘要，不是 CTF-Wiki 的一部分，也不适用 CC BY-NC-SA。摘要用自己的话归纳公开题解，并在每篇的 `sources` 与「参考链接」中保留原文 URL。原文、exploit 与附件的版权归原作者。

`templates/`、根目录 `README.md` 与本 `NOTICE.md` 是本仓库的说明文件。再分发 `wiki/` 时不要删掉本声明。
