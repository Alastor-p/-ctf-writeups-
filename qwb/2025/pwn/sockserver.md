# sockserver

## 题目信息
- 赛事：强网杯 2025 初赛
- 分类：Pwn

## 考点
- 类 SOCKS 协议的会话管理
- add/delete 索引不同步 → 覆盖 idx/ptr
- BSS 上伪造 link_map + ret2dlresolve
- 经内网 HTTP 服务取 flag 文件

## 解题思路
1. add 按 idx 判断，delete 直接 `--idx`，可制造指针错乱。
2. 伪造结构配合 main 中 gadget 实现任意写，把 ptr 扭到 BSS。
3. 在 BSS 伪造 link_map，改相关 GOT，ret2dl 解析到 `system`。
4. 利用 case 5 与后台 HTTP 交互，把命令结果写到 `flag.html` 再取回。

## 关键代码/payload
原文未给出可摘录的短代码，请参阅参考链接中的完整 exploit。

## 参考链接
- https://blog.wm-team.cn/index.php/archives/87/

> 本文为对公开 writeup 的归纳总结，版权归原作者所有；请务必阅读原文核对细节。
