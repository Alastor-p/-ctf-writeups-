---
title: 宇宙微波背景辐射
competition: 强网杯
year: 2026
category: Misc
tags: ['mkv', 'stego', 'temporal-correlation', 'ffmpeg']
sources: ['https://cn-sec.com/archives/5548779.html', 'https://github.com/CTF-Archives/2026-qwbs10-quals']
---

# 宇宙微波背景辐射


## 题目信息

- 赛事：第十届强网杯 2026 线上赛（Jeopardy）
- 分类：Misc
- 形态：离线附件（网盘 MKV，提取码 GAME）
- 公开解出：约 801 队（赛后榜统计）
- 题面：老式电视雪花噪声中约 1% 来自宇宙微波背景，提示“杂乱白噪声中残余秘密”

## 考点

- MKV / EBML 多轨与 Attachment 隐写
- 时间维相关性（相邻帧同像素稳定性）而非亮度阈值
- ffmpeg 无损抽轨 / dump_attachment

## 解题思路

公开 WP 指出附件是 MKV：`ffprobe` 可见主视频、整段雪花的隐藏视频轨、音轨、字幕轨，以及两个 Attachment（`g2.tar` / `g4.tar`）。六段文字材料分别藏在隐藏视频前后半、主视频尾部雪花、字幕与两份 tar 图片序列中。单帧看不出字形，因为笔画区域同样填满噪声；差别在时间维——背景每帧重随机，笔画像素跨帧被复制，相邻帧相同概率接近 1。对每像素统计相邻帧相等比例，再空间平滑即可积出文字，六段按语义拼成 flag。

## 关键代码/payload

短摘录（抽轨，来自公开 WP）：

```bash
ffmpeg -y -i challenge.mkv -map 0:1 -c copy hidden.mkv
ffmpeg -y -i challenge.mkv -map 0:s:0 hidden.srt
ffmpeg -y -dump_attachment:t "" -i challenge.mkv
```

## 参考链接

- https://cn-sec.com/archives/5548779.html
- https://github.com/CTF-Archives/2026-qwbs10-quals
