# Eternum

## 题目信息
- 赛事：CISCN 2025 初赛
- 分类：Misc

## 考点
- 自定义应用层帧 `ET3RNUMX` + 长度
- AES-GCM；密钥在样本硬编码
- 命令输出含 base32(flag)

## 解题思路
1. pcap 中 TCP payload 多帧拼接：魔数 8 字节 + u32be 长度 + body。
2. body = nonce(12) || ct || tag(16)；用样本内 32 字节 key 解密。
3. 下发命令含 `base32 /var/opt/...`，解码即 flag。

## 关键代码/payload
原文未给出可摘录的短代码，请参阅参考链接中的完整 exploit。

## 参考链接
- https://www.52pojie.cn/forum.php?mod=viewthread&tid=2083027

> 本文为对公开 writeup 的归纳总结，版权归原作者所有；请务必阅读原文核对细节。
