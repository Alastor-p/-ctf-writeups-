---
title: redisrelay
competition: 羊城杯
year: 2026
category: Pwn
tags: ['redis-module', 'multi-uid', 'uaf', 'tcache', 'protocol-chain']
sources: ['https://xz.aliyun.com/news/93035']
---

# redisrelay

## 题目信息

- 分类：PWN（HARD 级多 UID 链）
- 入口：Redis TCP + 模块 `redisrelay.so`
- 六层：module → relaybroker → routeattestor → routevault → routeledger → routecouncil（持有 flag fd）

## 考点

- 各层同构：随机 key 在 `.bss` 控制块；几乎每层都留「读控制块 / 写 .bss / UAF」口子
- 合法「关卡」常设计成走不通，必须用内存原语改 ready 标志或伪造 gate
- 隧道套隧道：seq 跨层接续、帧长上限、前缀由父进程代发

## 解题思路

1. **模块**：retire+ledger 复用泄露 key/基址；stampinfo 泄露 stamp；fragment/commit 武装后 `relay.tunnel`。
2. **broker**：UAF + 相对读；有符号索引写 route 头，过关连 attestor。
3. **attestor**：freed 块整块写 + 相对写直接改 `.bss` ready。
4. **vault**：字节码负索引读控制块；`lea rsp,[rdi+0x40];ret` 栈迁移。
5. **ledger / council**：manifest/有符号 idx 泄露 + tcache safe-linking 投毒写 gate；council 最终 `lseek/read` flag fd。

## 关键代码/payload

```text
# 高层: Redis 一连接 → 六层 ready/gate 全部伪造 → council op 读 fd4
# 完整帧格式与 MAC 公式见先知长文，不在此复述 exploit
```

## 参考链接

- https://xz.aliyun.com/news/93035
