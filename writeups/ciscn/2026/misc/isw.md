---
title: ISW 靶机链
competition: CISCN&长城杯半决赛
year: 2026
category: Misc
tags: ['isw', 'shiro', 'pwnkit', 'nfs', 'lateral']
sources:
  - 'https://www.cnblogs.com/lee0/p/19759628'
  - 'https://www.s1mh0.cn/blog/index.php/2026/03/25/2026ciscn/'
  - 'https://www.cnblogs.com/seyedog/p/19814241'
---

# ISW 靶机链

## 题目信息

- 分类：ISW（综合渗透）
- 多靶机 / 多 flag；公开 WP 覆盖入口 Web、提权、内网取证

## 考点

- Java 服务 + `rememberMe` → **Apache Shiro** 反序列化拿 WebShell
- 本地提权：**PwnKit**（CVE-2021-4034 / `pkexec`）
- 内网：NFS 挂载（如 `/nfsdir`）取 flag；另有 Agent 端口认证 RCE（公开复盘提及 12345）

## 解题思路

1. **flag1**：识别 Shiro，利用已知 gadget 反序列化读根目录 flag / 落 WebShell。
2. **提权**：上传并执行公开 PwnKit PoC（赛场环境 polkit 未修）。
3. **横向**：枚举 NFS / 内网服务，按题面取后续 flag。

> 仅记录公开链路级步骤；不粘贴完整 exploit / 恶意二进制。

## 关键代码/payload

```text
# 高阶链: Shiro RCE → webshell → pkexec LPE → NFS/Agent 取 flag
# PoC 仓库名可检索 CVE-2021-4034；具体命令见各队 WP
```

## 参考链接

- https://www.cnblogs.com/lee0/p/19759628
- https://www.s1mh0.cn/blog/index.php/2026/03/25/2026ciscn/
- https://www.cnblogs.com/seyedog/p/19814241
