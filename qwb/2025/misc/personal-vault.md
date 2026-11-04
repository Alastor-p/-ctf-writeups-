# Personal Vault

## 题目信息
- 赛事：强网杯 2025 初赛
- 分类：Misc

## 考点
- Windows 内存取证
- 关键字搜索 `flag{`（注意编码）

## 解题思路
1. 题目提供内存镜像；可用 WinDbg 定位 `personalVault` 相关进程/驱动。
2. 多份 WP 指出用文件搜索工具直接搜 UTF-16 的 `flag{` 即可非预期拿到 flag。

## 关键代码/payload
原文未给出可摘录的短代码，请参阅参考链接中的完整 exploit。

## 参考链接
- https://blog.wm-team.cn/index.php/archives/87/
- https://cn-sec.com/archives/4592147.html
- https://cn-sec.com/archives/4597169.html

> 本文为对公开 writeup 的归纳总结，版权归原作者所有；请务必阅读原文核对细节。
