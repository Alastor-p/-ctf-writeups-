---
title: misc04
competition: 网鼎杯
year: 2024
category: Misc
tags: [青龙, peano, image, qrcode]
sources:
  - https://mp.weixin.qq.com/s/HhL4lqcL_3EeYg1TDeBOKg
  - https://cn-sec.com/archives/3331560.html
  - https://www.cnblogs.com/backlion/p/18527653
  - https://github.com/CTF-Archives/2024-wdb-qinglong
---

# misc04

## 题目信息

- 赛事：第四届网鼎杯 2024 线上资格赛 · 青龙组
- 分类：Misc
- 题面：一张被自定义曲线打乱的图。题单见 [CTF-Archives](https://github.com/CTF-Archives/2024-wdb-qinglong)。

## 考点

- 皮亚诺（Peano）曲线还原像素
- 二维码

## 解题思路

公开文章把这题对上 IrisCTF 2024 的曲线置乱。递归生成 6 阶皮亚诺访问顺序，按这个顺序把原图像素填回一幅新图（纵坐标要按 `height-1-y` 翻一下）。还原图是二维码，扫码即 flag。曲线的具体递推和完整脚本在原文，这里不整段照搬。

## 关键代码/payload

```text
order = peano(6)
new[i%w, i//w] = img[x, height-1-y]
# 还原后扫二维码
```

## 参考链接

- https://mp.weixin.qq.com/s/HhL4lqcL_3EeYg1TDeBOKg
- https://cn-sec.com/archives/3331560.html
- https://www.cnblogs.com/backlion/p/18527653

> 本文为对公开 writeup 的归纳总结，版权归原作者所有；请务必阅读原文核对细节。
