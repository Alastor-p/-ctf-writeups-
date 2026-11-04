# tradre

## 题目信息
- 赛事：强网杯 2025 初赛
- 分类：Reverse

## 考点
- 父子进程 + ptrace 的 INT3 虚拟机
- AES-ECB + 可预测 rand 密钥链
- Frida 跟踪 handler

## 解题思路
1. 子进程布满 `__debugbreak`/`int3`，父进程按 handler 表解释控制流，不能随意下软断。
2. 用 Frida child gating 跟踪调用与基本块，还原出：`srand(0x10000)` 后 16 次 `rand` 作 AES key；第 17 次作新种子；再 32 字节作最终 XOR。
3. 明文对照串为 `Congratulations! This is the correct flag!`（注意第二块从偏移 17 比对，需去掉感叹号后多余空格）。
4. 按上述密钥派生逆 AES + XOR 得 flag。

## 关键代码/payload
```text
srand(0x10000); key = rand()*16; srand(rand()); xor_key = rand()*32; AES_decrypt then XOR
```

## 参考链接
- https://blog.wm-team.cn/index.php/archives/87/

> 本文为对公开 writeup 的归纳总结，版权归原作者所有；请务必阅读原文核对细节。
