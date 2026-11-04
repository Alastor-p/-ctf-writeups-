---
title: 谍影重重7
competition: 强网杯
year: 2026
category: Misc
tags: ['pcap', 'tls-keylog', 'rdp', 'restic', 'forensics']
sources: ['https://cn-sec.com/archives/5548779.html', 'https://github.com/CTF-Archives/2026-qwbs10-quals']
---

# 谍影重重7


## 题目信息

- 分类：Misc（流量取证 / 容器问答）
- 附件：`manager.pcap`、`internal.pcap`、`browser.keys`
- 公开解出：约 406 队

## 考点

- NSS key log 解密管理侧 HTTPS / VNC WebSocket
- RDP 驱动重定向重组文件
- Restic 仓库口令与保险库解密链

## 解题思路

公开 WP 将证据分成三层：用 `browser.keys` 解开 `manager.pcap` 的 TLS，还原 PVE 控制台 VNC（节点/VM、分辨率、笔记中的仓库口令线索）；在 `internal.pcap` 中定位 RDP（账户 `CORE01\Tsuki`），解密后经 RDPDR 重组 Restic 仓库；仓库快照含 `MouseVault.exe` 与 `core-assets.vault`，需把 RFB 鼠标事件与画面帧对齐还原数字键盘输入序列作为保险库口令，再 PBKDF2 + AES-CBC/HMAC 解出 SQLite 并校验哈希。多道填空题分别对应链路中间结论。

## 关键代码/payload

短摘录思路：TShark + TLS key log 解密；RDPDR `DEVICE_IO` 按 FileId/Offset 拼文件。具体脚本见公开 WP。

## 参考链接

- https://cn-sec.com/archives/5548779.html
