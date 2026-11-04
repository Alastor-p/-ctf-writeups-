---
title: catchme
competition: CISCN&长城杯半决赛
year: 2026
category: Pwn
tags: ['awdp', 'uaf', 'heap', 'patch']
sources:
  - 'https://www.cnblogs.com/seyedog/p/19814241'
---

# catchme

## 题目信息

- 分类：PWN / AWDP
- 公开复盘：delete 路径 `free` 后未清空 `heap[idx]` → UAF

## 考点

- Use-After-Free：指针悬挂可被后续分配复用
- AWDP：在有限补丁字节内消除 UAF（清空指针 / 跳过危险检查）

## 解题思路

### Break（高阶）

1. 触发 delete 留下悬空指针。
2. 再分配同尺寸块，覆写函数指针或关键元数据拿控制流（细节因二进制而异，见原文）。

### Fix（公开复盘要点）

- `free` 后将对应槽位置空；或 NOP 后续错误检查并插入清空指令；亦有跳转 EH_FRAME 完成清空的赛场手法。

## 关键代码/payload

```text
# 高阶: free(heap[i]); heap[i]=NULL;
# 完整 exploit / 补丁字节流见赛后复盘，此处不复述
```

## 参考链接

- https://www.cnblogs.com/seyedog/p/19814241
