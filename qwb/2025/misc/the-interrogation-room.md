# The_Interrogation_Room

## 题目信息
- 赛事：强网杯 2025 初赛
- 分类：Misc

## 考点
- 交互式 PoW
- 对囚犯做布尔查询（异或/奇偶校验矩阵）
- 带噪声的秘密比特还原

## 解题思路
1. 先解 sha256 PoW。
2. 按给定 0/1 矩阵构造「若干变量异或」式提问，收集 True/False 响应。
3. 在最多少量错误的前提下，枚举 8-bit 秘密与观测向量的汉明距离，唯一解码后回传比特串，多轮后得 flag。

## 关键代码/payload
原文未给出可摘录的短代码，请参阅参考链接中的完整 exploit。

## 参考链接
- https://blog.wm-team.cn/index.php/archives/87/
- https://cn-sec.com/archives/4592147.html

> 本文为对公开 writeup 的归纳总结，版权归原作者所有；请务必阅读原文核对细节。
