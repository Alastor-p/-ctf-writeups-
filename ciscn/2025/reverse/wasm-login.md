# wasm-login

## 题目信息
- 赛事：CISCN 2025 初赛
- 分类：Reverse

## 考点
- 浏览器 CORS 限制加载 WASM
- 自定义 Base64 + 非标准 HMAC-SHA256
- 爆破 Date.now 毫秒时间戳
- MD5(JSON) 前缀校验

## 解题思路
1. 本地需关闭浏览器同源策略才能加载附件 WASM；HTML 注释给出 admin/admin。
2. `authenticate` 用时间戳参与签名；前端对 `JSON.stringify(authData)` 做 MD5，要求前缀 `ccaf33e3512e31f3`。
3. 按题目提示的周末/构建时间窗口爆破毫秒戳（或 hook `Date.now`），命中 `1766334550699`。
4. 对应 check 即为 flag 内容。

## 关键代码/payload
```javascript
TARGET = "ccaf33e3512e31f3"; # brute ts until md5(JSON.stringify(authenticate("admin","admin"))).startswith(TARGET)
```

## 参考链接
- https://l0serqianxia.github.io/blog/2025/12/29/ciscn-2025-personal-writeup/
- https://moyuin.top/blog/%E9%95%BF%E5%9F%8E%E6%9D%AF%20WriteUP
- https://www.52pojie.cn/forum.php?mod=viewthread&tid=2083027
- https://godownio.github.io/2025/12/20/2025-ciscn-chu-sai-wp-by-yp0int/

> 本文为对公开 writeup 的归纳总结，版权归原作者所有；请务必阅读原文核对细节。
