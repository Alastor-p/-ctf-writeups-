---
title: InkVerse
competition: DASCTF夏季赛
year: 2026
category: Web
tags: ['flask', 'toctou', 'race', 'rbac']
sources:
  - 'https://j-0k3r.github.io/2026/06/01/2026DASCTF夏季赛/'
---

# InkVerse

## 题目信息

- 分类：WEB（博客社区）
- 文档：`/api/docs`；角色 user → reviewer（声望≥50）→ featured_author / admin

## 考点

- `/api/tip`：**余额检查与扣款之间 TOCTOU**，并发打赏可透支余额刷声望
- 导出文章泄露 `Feature-Token`；签名请求精选文章升 `featured_author`
- Flask session 密钥强度足够，字典打不穿（公开 WP 结论）

## 解题思路

1. 注册登录；对同一文章并发大量 tip，声望破 50 升 reviewer。
2. 第二账号互审通过文章；导出拿 Feature-Token，请求 feature。
3. 进入 bulletin 等后续链路（digest/import 等细节见原文合集；本摘要覆盖至 featured 主链）。

## 关键代码/payload

```python
# 并发 tip 示意
with ThreadPoolExecutor(30) as ex:
    list(ex.map(lambda _: session.post(f"{BASE}/api/tip", json={"article_id": 1}), range(30)))
```

## 参考链接

- https://j-0k3r.github.io/2026/06/01/2026DASCTF夏季赛/
