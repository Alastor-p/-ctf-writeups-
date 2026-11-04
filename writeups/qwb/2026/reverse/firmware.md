---
title: firmware
competition: 强网杯
year: 2026
category: Reverse
tags: ['firmware', 'ota', 'verification']
sources: ['https://cn-sec.com/archives/5548848.html', 'https://github.com/CTF-Archives/2026-qwbs10-quals']
---

# firmware


## 题目信息

- 分类：Reverse
- 附件：`qwb2026_firmware.tar.gz`
- 公开解出：约 438 队

## 考点

- 固件镜像 / OTA 分段拼接
- 自校验与 twin-fw 验证逻辑

## 解题思路

公开 WP：解析固件包中的验证路径（日志可见 `twin-fw: verification ok`），从 OTA 某偏移起的分段拼出短固件程序，再对照主程序对 keymat 的自校验恢复密钥或明文，最终得到 flag。细节步骤与偏移以源文表格为准。

## 关键代码/payload

短摘录：按 WP 所述从 OTA `0x3c` 起拼接约 38 字节固件程序后再做校验逆。

## 参考链接

- https://cn-sec.com/archives/5548848.html
