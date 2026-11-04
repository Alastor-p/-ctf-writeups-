# SnakeBackdoor（系列）

## 题目信息
- 赛事：CISCN 2025 初赛
- 分类：Misc

## 考点
- HTTP 爆破与 SSTI 流量
- Flask SECRET_KEY
- 多层 base64/zlib 还原 RC4 key
- 二进制后门随机密钥与 SM4 会话

## 解题思路
1. 1：过滤 `/admin/login` POST，最后一次成功密码 `zxcvbnm123`。
2. 2：登录后 SSTI 读 `config`，得到 SECRET_KEY。
3. 3：对注入 payload 反复 base64/反转/zlib，见到 RC4 与 key 字符串。
4. 4–5：还原攻击者下载的 zip（密码见于流量），逆向木马；C2 下发 4 字节作 srand 种子生成通信 key。
5. 6：会话为 SM4；把密文重放给样本或自实现解密，注意 flag 中有字符替换需还原。

## 关键代码/payload
原文未给出可摘录的短代码，请参阅参考链接中的完整 exploit。

## 参考链接
- https://l0serqianxia.github.io/blog/2025/12/29/ciscn-2025-personal-writeup/
- https://godownio.github.io/2025/12/20/2025-ciscn-chu-sai-wp-by-yp0int/
- https://www.52pojie.cn/forum.php?mod=viewthread&tid=2083027

> 本文为对公开 writeup 的归纳总结，版权归原作者所有；请务必阅读原文核对细节。
