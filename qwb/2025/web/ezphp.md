# ezphp

## 题目信息
- 赛事：强网杯 2025 初赛
- 分类：Web

## 考点
- PHP 反序列化 / 动态调用
- 匿名类 `readflag` 魔术调用（参考 p 牛 2023 题）
- phar 文件名碰撞绕过 include 过滤
- SUID + base64 读 flag

## 解题思路
1. 通过序列化 `test` 对象触发 `phpinfo`，确认 `disable_functions` 较严。
2. 构造含 `readflag` 的对象，利用匿名类函数名 `\0readflag/<file>:<line>$N` 触发内层逻辑（注意 eval'd code 的文件名与计数器）。
3. include 过滤难以直接竞争时，爆破 `mt_srand` 种子使随机文件名以 `phar` 开头，再上传 gzip phar 触发。
4. 拿到 webshell 后利用环境中的 SUID 工具（如 base64）读取 `/flag`。

## 关键代码/payload
```php
O:4:"test":3:{s:8:"readflag";N;s:1:"f";s:4:"test";s:3:"key";s:5:"class";}
```

## 参考链接
- https://blog.wm-team.cn/index.php/archives/87/

> 本文为对公开 writeup 的归纳总结，版权归原作者所有；请务必阅读原文核对细节。
