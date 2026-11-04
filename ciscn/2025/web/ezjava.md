# EzJava

## 题目信息
- 赛事：CISCN 2025 初赛
- 分类：Web

## 考点
- Thymeleaf 服务端模板注入
- 禁用 `T(...)` / `new`，用反射调静态方法读文件

## 解题思路
1. 弱口令登录后台后发现模板渲染点。
2. `T` 与 `new` 被过滤，改用 `''.getClass.forName(...).getMethod(...).invoke(...)`。
3. 经 `URI.create` → `toURL().openStream()` 得到 InputStream，再用 `StreamUtils.copyToString` 回显；`flag` 关键字可用 `#strings.concat` 拆开。

## 关键代码/payload
```text
[[${''.getClass.forName("org.springframework.util.StreamUtils").getMethod("copyToString", ...).invoke(null, ..., UTF_8)}]]
```

## 参考链接
- https://godownio.github.io/2025/12/20/2025-ciscn-chu-sai-wp-by-yp0int/
- https://luo-kaihong.github.io/p/2025-ciscn%E5%88%9D%E8%B5%9B/

> 本文为对公开 writeup 的归纳总结，版权归原作者所有；请务必阅读原文核对细节。
