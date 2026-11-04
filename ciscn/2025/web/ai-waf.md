# AI_WAF

## 题目信息
- 赛事：CISCN 2025 初赛
- 分类：Web

## 考点
- WAF 关键词过滤
- MySQL `/*!50000...*/` 内联注释绕过
- 联合注入读库

## 解题思路
1. 普通 `union select` 被拦；fuzz 后发现带特定标记（如 NexaData）或内联注释时过滤变弱。
2. 用 `/*!50000union*/ /*!50000select*/` 等取出 `information_schema` 表字段，再读 flag 表。
3. 另一种写法在条件后追加 `||` 绕过字段名检测。

## 关键代码/payload
```sql
' /*!50000union*/ /*!50000select*/ 1,2,flagcol from flagtable -- -
```

## 参考链接
- https://godownio.github.io/2025/12/20/2025-ciscn-chu-sai-wp-by-yp0int/
- https://luo-kaihong.github.io/p/2025-ciscn%E5%88%9D%E8%B5%9B/

> 本文为对公开 writeup 的归纳总结，版权归原作者所有；请务必阅读原文核对细节。
