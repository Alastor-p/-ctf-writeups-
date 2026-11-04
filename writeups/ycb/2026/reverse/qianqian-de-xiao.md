---
title: 千千的咲
competition: 羊城杯
year: 2026
category: Reverse
tags: ['android', 'unreal', 'wasm', 'vm', 'arx']
sources: ['https://xz.aliyun.com/news/93035', 'https://xz.aliyun.com/news/93039']
---

# 千千的咲

## 题目信息

- 分类：逆向 / Android（UE + Puerts/WASM + 原生 VM）
- 附件：APK + `libUnreal.so`；资源 `main.obb.png` 实为 ZIP
- Flag 样例：`flag{WuTher1ng_Waves_ch1Sak1_6666}`

## 考点

- `p.bin` XTEA-CBC（key `qianqiandexiao99`）→ WASM；导入 `q` 调原生分发器
- 493 块点击表；四轮可逆 ARX 打包 8 次点击；需边跑边解（块号链表 + V 依赖摘要）
- 终局 SHA256 派生 key/iv；**魔改 AES**，宜仿真原生解密 + FNV 校验

## 解题思路

1. 解资源拿 `p.bin`，解密 WASM；补丁反调试。
2. 探针拿块头密钥 V，`Tinv` 解出格号序列共 3941 次，真跑 WASM+原生。
3. 完成态取 salt/engine，派生 key/iv，调原生解密得 flag。

## 关键代码/payload

```python
# 四轮变换可逆（示意）
def Tinv(y, a, b, c):
    for i in reversed(range(4)):
        # mul_inv / ror / sub / xor 见原文
        ...
```

## 参考链接

- https://xz.aliyun.com/news/93035
- https://xz.aliyun.com/news/93039
