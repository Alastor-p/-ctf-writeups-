---
title: TaxManager
competition: DASCTF夏季赛
year: 2026
category: Web
tags: ['java', 'deserialization', 'freemarker', 'xxe', 'rbac']
sources:
  - 'https://j-0k3r.github.io/2026/06/01/2026DASCTF夏季赛/'
---

# TaxManager

## 题目信息

- 分类：WEB（Java Spring Boot 税务系统）
- 密钥硬编码：`api.signing.secret=TaxManager_Secret_K3y_2026_Un1que`

## 考点

- Profile 反射改字段：禁 `role=admin` 但允许 `role=reviewer`
- 审核附件经 HMAC 后写入 `voucherData`；导出路径不安全反序列化
- 自研链：`ScheduledTaskHandler.readObject` → `ReportJob.run` → FreeMarker SSTI
- XXE 在 import；SSTI 无回显时写 `/tmp` 再 XXE 读出（公开手法）

## 解题思路

1. 提权 reviewer；申请退税。
2. 本地构造 `ScheduledTaskHandler` gadget（Freemarker ObjectConstructor 写 base64 flag 到临时文件）。
3. HMAC-SHA256 签名后 `POST /api/review` approve 带 `attachmentData`。
4. `export/prepare` + `generate` 触发反序列化；XXE 读临时文件。

## 关键代码/payload

```text
# Gadget: ScheduledTaskHandler → ReportJob → PdfReportGenerator.render(SSTI)
# secret: TaxManager_Secret_K3y_2026_Un1que
# SSTI 示意: ObjectConstructor → ProcessBuilder → cat /f* | base64 >/tmp/b64
```

完整序列化 blob 见原文，此处不粘贴超长 Base64。

## 参考链接

- https://j-0k3r.github.io/2026/06/01/2026DASCTF夏季赛/
