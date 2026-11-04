---
title: 0perator
competition: 强网杯
year: 2026
category: Misc
tags: ['vnc', 'kiosk', 'dbus', 'component-signing']
sources: ['https://cn-sec.com/archives/5548779.html', 'https://github.com/CTF-Archives/2026-qwbs10-quals']
---

# 0perator


## 题目信息

- 分类：Misc（容器 / VNC 桌面）
- 目标：读取 `/root/flag.txt`
- VNC 密码题面给出：`123qwe123`
- 公开解出：约 285 队

## 考点

- Chromium kiosk 逃逸到本地 shell
- 设备管理器组件覆盖目录可写
- Python 组件验签只校验清单签名、不绑定内容哈希（`include_sha256=False`）

## 解题思路

入口是 RFB VNC，桌面为酒店自助入住 kiosk（Flask + root 设备管理器经 D-Bus）。完整业务流（TOTP→入住→人脸）因无摄像头走不通。公开链：屏幕二维码泄漏 TOTP 密钥 → `Super+E` 打开文件管理器拿到 kiosk shell → 利用 `/var/lib/0perator/components/user` 可写覆盖面组件；Python 组件验签不绑内容哈希，配合可写 `face.status` 与允许 kiosk 调用的 `ReloadComponents`，让 root 管理器加载恶意 `face.py` 从而读 flag。

## 关键代码/payload

（公开 WP 以交互步骤为主；核心是覆盖用户组件目录并触发 ReloadComponents。此处不复述完整恶意组件代码。）

## 参考链接

- https://cn-sec.com/archives/5548779.html
