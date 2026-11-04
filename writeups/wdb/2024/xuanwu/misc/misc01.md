---
title: misc01
competition: 网鼎杯
year: 2024
category: Misc
tags: [玄武, dfir, tomcat, webshell]
sources:
  - https://1cepeak.cn/posts/wdb2024-turtle-writeup/
---

# misc01

## 题目信息

- 赛事：第四届网鼎杯 2024 线上资格赛 · 玄武组
- 分类：Misc
- 题面：应急十连问。附件是一份 pcapng，加上 Foxmail 与 Windows 用户目录的压缩包。1cePeak 的原文把本题标成 MISC01，同文的 MISC02 是钓鱼与远控，见同目录另一篇。

## 考点

- Tomcat 弱口令与 `server.xml` / WAR 落地
- JSP webshell 的 XOR + AES，以及按 TCP 流解密
- .NET 勒索样本加密的后缀列表，和解 `secret.txt.locked`

## 解题思路

十问串在同一条 Tomcat 入侵上。公开文章的调查顺序是：

1. `conf/tomcat-users.xml` 里的管理员口令。
2. 恶意包落在 Tomcat 的 `conf`（文中答案路径指向 `server.xml` 这一问的格式要求）。
3. `control.jsp` 里两套加密是 XOR 和 AES，密钥写在脚本里。流量按这两套解开。
4. 某一条 TCP 流是删除 Foxmail 临时目录里的 `install_guide.pdf.lnk`，按题目要求提交路径的 MD5。
5. 另一条流上传 `downloadCache`，再下一条是 `certutil -decode` 把它变成 exe。题目要的是命令行的 MD5，不是命令原文。
6. 更后面的分块流量拼出 `hw-view.exe`。dnSpy 里能看到它加密的后缀，按字母序用下划线接起来。
7. 外联 URL 以流量为准，是内网地址。
8. 按样本里的算法解密 `secret.txt.locked`。文中明文是 `flag{Y0u_4re_MASTER_0f_DFIR}`，再按题目要求做 MD5。

答完十问后，1cePeak 贴出的容器 flag 是 `wdflag{See_U_Again_WDB2026}`。每一问的提交串以原文为准，这里不逐条抄。

## 关键代码/payload

```text
tomcat-users.xml → control.jsp 的 XOR 与 AES
按 TCP 流解密：删除的 lnk、上传的 class、certutil、hw-view.exe
dnSpy 看加密后缀；解密 secret.txt.locked
```

## 参考链接

- https://1cepeak.cn/posts/wdb2024-turtle-writeup/

> 本文为对公开 writeup 的归纳总结，版权归原作者所有；请务必阅读原文核对细节。
