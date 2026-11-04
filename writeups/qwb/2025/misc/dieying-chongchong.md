---
title: "谍影重重 6.0"
competition: "强网杯"
year: 2025
category: "Misc"
tags:
  - "pcap 中 RTP over UDP 音频"
  - "八进制串还原压缩包密码"
  - "历史事件梗 → md5(时间地点)"
sources:
  - "https://cn-sec.com/archives/4592147.html"
  - "https://blog.wm-team.cn/index.php/archives/87/"
---
# 谍影重重 6.0

## 题目信息
- 赛事：强网杯 2025 初赛
- 分类：Misc

## 考点
- pcap 中 RTP over UDP 音频
- 八进制串还原压缩包密码
- 历史事件梗 → md5(时间地点)

## 解题思路
1. 流量含大量 UDP，识别为 RTP；用 tshark 按 SSRC 抽 payload 转 wav。
2. 长音频降噪/清空白后转写，得到「第九届强网杯」相关八进制数字串，按贪心拼 ASCII 得 zip 密码。
3. 解压文案指向金门战役梗：时间「辰时正过三刻」、地点「双鲤湖西岸南山茶铺」→ `1949年10月24日8时45分于双鲤湖西岸南山茶铺`，再 md5 得 flag。

## 关键代码/payload
```text
flag = md5('1949年10月24日8时45分于双鲤湖西岸南山茶铺')
```

## 参考链接
- https://cn-sec.com/archives/4592147.html
- https://blog.wm-team.cn/index.php/archives/87/

> 本文为对公开 writeup 的归纳总结，版权归原作者所有；请务必阅读原文核对细节。
