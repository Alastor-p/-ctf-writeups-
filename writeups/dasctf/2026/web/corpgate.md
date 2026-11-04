---
title: CorpGate
competition: DASCTF夏季赛
year: 2026
category: Web
tags: ['prototype-pollution', 'jwt', 'nodejs', 'rce']
sources:
  - 'https://j-0k3r.github.io/2026/06/01/2026DASCTF夏季赛/'
---

# CorpGate

## 题目信息

- 分类：WEB
- 栈：Node/Express/EJS + JWT；诊断接口 `execSync('/readflag')`（需 admin + 一次性 reference）

## 考点

- `deepMerge`：`BLOCKED_ROOTS` 仅在 `depth<3` 生效 → 深度≥3 可写 `constructor.prototype`
- 污染 `Object.prototype.pending` 后，无认证 `healthcheck` 触发 `configRefresh`，把 JWT 签名密钥换成攻击者控制值
- 伪造 `role=admin` JWT → 取 diagnostic reference → 执行读 flag

## 解题思路

1. 注册拿 employee JWT。
2. `POST /api/settings` 嵌套 `notifications.digest.channels.constructor.prototype.pending = "<key>"`。
3. `GET /api/system/healthcheck` 轮换密钥；用新密钥签 admin JWT。
4. 管理面板取 reference，`POST /api/reports/execute` 得 flag。

## 关键代码/payload

```json
{
  "notifications": {
    "digest": {
      "channels": {
        "constructor": { "prototype": { "pending": "passwd" } }
      }
    }
  }
}
```

## 参考链接

- https://j-0k3r.github.io/2026/06/01/2026DASCTF夏季赛/
