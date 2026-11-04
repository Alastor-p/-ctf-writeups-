---
title: license
competition: 强网杯
year: 2026
category: Reverse
tags: ['whitebox-aes', 'vm', 'anti-debug', 'feistel']
sources: ['https://eryuemu.com/blog/qwb-2026-neuron-shuffle-license-recap/', 'https://cn-sec.com/archives/5548848.html']
---

# license


## 题目信息

- 分类：Reverse
- 附件：静态链接 x86-64 ELF
- 输入：96 个大写 hex（48 字节 license）
- 公开解出：约 473 队

## 考点

- 白盒 AES 诱饵与无效 fold
- 反调试 / 自校验下的零侵入采样（`/proc/pid/mem`）
- 自修改 VM、Feistel 哈希反演、逐字符枚举

## 解题思路

公开预期解：白盒校验结果对 VM 无实质影响；gdb/ptrace 会破坏密钥流。用父进程读 `/proc/<pid>/mem` 采样 ctx。前 24 字节经 3 路 8 字节 Feistel + 线性 `FIN` 与目标比较；后 24 字节逐字节影响密钥流。补全仿真器 LOOP 族后逐字符搜索；`Rejected.` 实为崩溃兜底而非判定。真机喂入完整 license 打印 flag（公开复验形如 UUID）。

## 关键代码/payload

```text
# 真机验证形态（license 为 96 hex，具体值见源文）
./license < TRUE_LIC.txt
# => flag{...}
```

## 参考链接

- https://eryuemu.com/blog/qwb-2026-neuron-shuffle-license-recap/
- https://cn-sec.com/archives/5548848.html
