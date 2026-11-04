---
title: "dialects"
competition: "DEF CON CTF Qualifier"
year: 2025
category: "Crypto"
tags:
  - "TLS（stdin/stdout 包装）"
  - "国密 SM4-CTR / SM3，但 S 盒/初值/旋转被出题方魔改"
  - "cmd2：SM3(data\\|nonce) 前 3 字节为 0"
  - "cmd1：SHA512(data\\|nonce) 特定前缀后读文件"
sources:
  - "https://blog.cloudlabs.ufscar.br/sec/defcon-quals-2025/"
  - "https://github.com/Nautilus-Institute/quals-2025/tree/main/dialects"
  - "https://ctfpal.com/writeups/ctf/def-con-ctf-qualifier-2025-2604"
---
# dialects

## 题目信息
- 赛事：DEF CON CTF Qualifier 2025
- 分类：Crypto

## 考点
- TLS（stdin/stdout 包装）
- 国密 SM4-CTR / SM3，但 S 盒/初值/旋转被出题方魔改
- cmd2：SM3(data\|nonce) 前 3 字节为 0
- cmd1：SHA512(data\|nonce) 特定前缀后读文件

## 解题思路
1. 握手后双方各贡献 8 字节组成 16 字节 SM4-CTR key；IV 全零。
2. 标准 OpenSSL SM3/SM4 对不上，需从二进制抽出魔改实现（或 ptrace/patch 出 keystream）。
3. 先发 cmd2 做 SM3 前缀 PoW，再发 cmd1 做 SHA512 前缀校验，最后加密发送 `./flag.txt` 路径读取。
4. 线上需在 TLS 前先交 Nautilus ticket，再用 `SSLContext.wrap_socket` 升级连接。

## 关键代码/payload
```text
# 流程: TLS -> share key -> SM4-CTR
# cmd2: brute x: SM3(x||nonce)[:3]==0
# cmd1: brute y: SHA512(y||nonce) startswith 8d3600
# then read ./flag.txt
```

## 参考链接
- https://blog.cloudlabs.ufscar.br/sec/defcon-quals-2025/
- https://github.com/Nautilus-Institute/quals-2025/tree/main/dialects
- https://ctfpal.com/writeups/ctf/def-con-ctf-qualifier-2025-2604

> 本文为对公开 writeup 的归纳总结，版权归原作者所有；请务必阅读原文核对细节。
