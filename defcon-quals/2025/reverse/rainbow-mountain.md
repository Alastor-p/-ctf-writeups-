# rainbow mountain (rbm)

## 题目信息
- 赛事：DEF CON CTF Qualifier 2025
- 分类：Reverse

## 考点
- 静态链接、Debian bookworm 工具链痕迹
- 巨大函数指针表，选 index 后喂 base64
- 网格拷贝后比较相邻 `target` 与 `wanted`
- 需找到可溢出且输入为回文的变体函数

## 解题思路
1. 程序 `fill_func_arr` 后让选手选函数下标，再 base64 解码作为参数。
2. 多数函数把输入按蛇形写入 `arr` 再比 `target`；自动化搜「拷贝长度 ≥ arr+8」的变体。
3. 命中的函数在拷贝前要求输入为**回文**，且可拷贝 72 字节到 64 字节缓冲，刚好覆盖 8 字节 `wanted`。
4. 构造 `wanted[::-1] + padding + wanted` 的回文 payload，选对应 index（原文为 1576）提交。

## 关键代码/payload
```python
wanted = p64(0x3447784339354946)
payload = base64(wanted[::-1] + b'A'*(64-8) + wanted)
```

## 参考链接
- https://blog.cloudlabs.ufscar.br/sec/defcon-quals-2025/
- https://github.com/Nautilus-Institute/quals-2025/tree/main/rbm
- https://ctfpal.com/writeups/ctf/def-con-ctf-qualifier-2025-2604

> 本文为对公开 writeup 的归纳总结，版权归原作者所有；请务必阅读原文核对细节。
