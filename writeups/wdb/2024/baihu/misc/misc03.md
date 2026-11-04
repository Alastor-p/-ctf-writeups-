---
title: misc03
competition: 网鼎杯
year: 2024
category: Misc
tags: [白虎, php-filter, side-channel, pcap]
sources:
  - https://mp.weixin.qq.com/s/5Xet54leUqVOeMYzTX0ROw
  - https://sechub.in/view/2964737
  - https://www.cnblogs.com/backlion/p/18527653
  - https://boogipop.com/2023/05/08/Web%E4%BE%A7%E4%BF%A1%E9%81%93%E5%88%9D%E6%AD%A5%E8%AE%A4%E8%AF%86/
---

# misc03

## 题目信息

- 赛事：第四届网鼎杯 2024 线上资格赛 · 白虎组
- 分类：Misc
- 题面：内网被攻击后的流量。见 [CTF-Archives 白虎题单](https://github.com/CTF-Archives/2024-wdb-baihu)。

## 考点

- PHP `iconv` / `convert` 过滤器的报错侧信道
- 离线流量代替在线 HTTP 预言机

## 解题思路

流量形态对得上 DownUnderCTF 2022 `minimal-php` 那类 oracle：不同 filter 链会让状态码不同，从而逐字节漏出文件。公开 WP 不再向靶机发请求，而是用 tshark 把包里的 `value` 和对应状态码收成字典，替换原脚本的 `req()`。

为了让离线数据对上，文中把放大过滤器改成重复 3000 次 `convert.quoted-printable-encode`，并在链里加上 `convert.iconv..CSISO2022KR`。跑完字典即可得到 flag。完整 oracle 脚本在原文和所引用的侧信道笔记里。

## 关键代码/payload

```text
tshark 导出 (filter 参数, 状态码) → 本地字典
blow_up = quoted-printable-encode × 3000
chain 含 convert.iconv..CSISO2022KR
```

## 参考链接

- https://sechub.in/view/2964737
- https://www.cnblogs.com/backlion/p/18527653
- https://boogipop.com/2023/05/08/Web%E4%BE%A7%E4%BF%A1%E9%81%93%E5%88%9D%E6%AD%A5%E8%AE%A4%E8%AF%86/

> 本文为对公开 writeup 的归纳总结，版权归原作者所有；请务必阅读原文核对细节。
