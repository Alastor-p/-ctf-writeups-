---
title: vmshare
competition: 强网杯
year: 2026
category: Crypto
tags: ['avx2', 'mitm', 'prng', 'simd']
sources: ['https://github.com/xiaoshabi-cmd/qiangwangbei2026', 'https://cn-sec.com/archives/5548779.html']
---

# vmshare


## 题目信息

- 分类：Crypto（题名亦作 SIMD_TINY_BLOCK_IS_A_NIGHTMARE）
- 附件：`encryptor`（AVX2 ELF）+ `cipher.bin`（32 B）
- Flag 格式：`flag{XXXXXXX_YYYYYYY}`（两组 7 位十六进制）
- 公开解出：约 899 队

## 考点

- AVX2 轮函数可逆建模
- 48-bit 密钥中间相遇
- PRNG 丢弃高 4 bit 导致 flag 高半字节需平台 oracle

## 解题思路

逆向得：两组 28-bit hex 经 `prng`（只保留低 24 bit）生成密钥字，再对 IV `"SIMD_TINY_BLOCK_IS_A_NIGHTMARE!!"` 做两轮可逆 SIMD 变换。对 X/Y 各 2²⁴ 做 MITM，约 20s 得唯一低 24 bit。因高 4 bit 不进入密文，需缩小候选后用提交接口确定完整 7 位 hex（公开 WP 记录命中 `flag{3174812_31af718}`）。

## 关键代码/payload

```c
// 思路：枚举 X 建 S1 表，枚举 Y 逆推查表（见源仓库 solve.c）
```

## 参考链接

- https://github.com/xiaoshabi-cmd/qiangwangbei2026/blob/main/vmshare_6d3416fb746f85cad8020e41571f8b7b/writeup.md
- https://cn-sec.com/archives/5548779.html
