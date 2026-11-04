---
title: misc02
competition: 网鼎杯
year: 2024
category: Misc
tags: [玄武, phishing, xenorat, aes]
sources:
  - https://1cepeak.cn/posts/wdb2024-turtle-writeup/
  - https://www.ctfiot.com/214152.html
  - https://sechub.in/view/2966475
---

# misc02

## 题目信息

- 赛事：第四届网鼎杯 2024 线上资格赛 · 玄武组
- 分类：Misc
- 题面：又是十连问，和 misc01 共用同一份主机目录与流量。ChaMd5 把本题标成 misc2，1cePeak 标成 MISC02。

## 考点

- 钓鱼邮件对应 ATT&CK T1566
- LNK 的目标命令和 SID
- HTA 释放的远控是 XenoRAT，流量为 AES-CBC

## 解题思路

公开文章的十条是一条钓鱼链：

1. 初始访问是钓鱼，技术编号 T1566。
2. Foxmail 最新一封邮件里的附件是 lnk。属性里的目标是 `mshta.exe` 拉一个 hta；用十六进制看 lnk 能读到 SID。提交格式是 `lnk_<SID>`。
3. 上一问的目标命令就是第 3 问的答案，不写全路径。
4. 全盘搜 `.hta`，缓存目录在 IE 的 `Content.IE5` 下。
5. hta 下载 `Flycode_VPN_installer.exe`，dnSpy 解掉里面的 Base64，得到的仍是 exe，再反编译，框架名是 xenorat。
6. 加解密函数是 AES。de4dot 去掉混淆后，在程序里能看到回连地址和密钥。
7. 沙箱或解密后的配置给出 `172.25.136.161:10004`。
8. 硬件编号不在样本里，而在 C2 回包。公开脚本用 AES-CBC、全零 IV 解流量（跳过每条记录前面的长度头），回包里有硬件号。
9. 被继续利用的正常应用是目录里的 `apache tomcat 10.1.25`。
10. webshell 包是 `host.war`。

具体提交串以 1cePeak / ChaMd5 原文为准。

## 关键代码/payload

```text
Foxmail → install.hta 的 lnk → T1566 / SID / mshta
dnSpy → xenorat，AES-CBC（IV 为 16 字节 0）
解密 C2 回包得到硬件号
```

## 参考链接

- https://1cepeak.cn/posts/wdb2024-turtle-writeup/
- https://www.ctfiot.com/214152.html
- https://sechub.in/view/2966475

> 本文为对公开 writeup 的归纳总结，版权归原作者所有；请务必阅读原文核对细节。
