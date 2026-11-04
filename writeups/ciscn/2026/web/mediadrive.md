---
title: MediaDrive
competition: CISCN&长城杯半决赛
year: 2026
category: Web
tags: ['php', 'unserialize', 'iconv', 'awdp', 'lfi']
sources:
  - 'https://lengkur.github.io/2026/04/16/wp/ciscn2026/MediaDrive/'
  - 'https://www.cnblogs.com/lee0/p/19759628'
---

# MediaDrive

## 题目信息

- 分类：WEB / AWDP
- 栈：PHP；Cookie `user` 反序列化 `User`
- `User` 可控字段：`name` / `encoding` / `basePath`（默认 uploads）

## 考点

- `preview.php`：`$rawPath = $user->basePath . $_GET['f']`
- **先**正则拦 `flag`/`..`/伪协议，**再** `iconv($encoding, "UTF-8//IGNORE", $rawPath)` 后 `file_get_contents`
- `//IGNORE` 可丢弃特殊字节（如 `€`、UTF-7 不可映射字符）→ 过滤与最终路径不一致

## 解题思路

### Break

1. Cookie 伪造 `User`：`basePath=/`，`encoding` 选 `UTF-7` 或 `ISO-2022-CN-EXT` 等。
2. `f` 取 `f€lag`（或在 `flag` 中插入无法映射字符），正则看不到完整 `flag`。
3. iconv 丢弃干扰字节后路径变为 `/flag`，读出内容。

### Fix（公开 WP 共识）

- 删除或硬编码 `basePath`；先转码再白名单校验；禁止用户控 encoding。

## 关键代码/payload

```php
class User {
  public string $name = "guest";
  public string $encoding = "ISO-2022-CN-EXT"; // 或 UTF-7
  public string $basePath = "/";
}
# GET preview.php?f=f€lag
```

## 参考链接

- https://lengkur.github.io/2026/04/16/wp/ciscn2026/MediaDrive/
- https://www.cnblogs.com/lee0/p/19759628
