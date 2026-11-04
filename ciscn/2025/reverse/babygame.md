# babygame

## 题目信息
- 赛事：CISCN 2025 初赛
- 分类：Reverse

## 考点
- Godot 游戏
- GDRETools 解包 `.gd` 脚本
- 收集金币后 AES key 被替换字符

## 解题思路
1. 用 GDRETools 解包，在 `flag.gd` 见到 AES-ECB 与密文 `d458af70...`、初始 key `FanAglFanAglOoO!`。
2. `game_manager.gd` 在得分后把 key 里的 `A` 换成 `B` → `FanBglFanBglOoO!`。
3. 用新 key 解密得 `flag{wOW~youAregrEaT!}}`。

## 关键代码/payload
```python
key = b"FanBglFanBglOoO!"; AES_ECB_decrypt(bytes.fromhex("d458af702a680ae4d089ce32fc39945d"), key)
```

## 参考链接
- https://l0serqianxia.github.io/blog/2025/12/29/ciscn-2025-personal-writeup/
- https://godownio.github.io/2025/12/20/2025-ciscn-chu-sai-wp-by-yp0int/
- https://www.52pojie.cn/forum.php?mod=viewthread&tid=2083027

> 本文为对公开 writeup 的归纳总结，版权归原作者所有；请务必阅读原文核对细节。
