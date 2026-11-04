# Qcalc

## 题目信息
- 赛事：强网杯 2025 初赛
- 分类：Misc

## 考点
- Android deeplink `qiangcalc://`
- 异常路径把 Intent 交给 BridgeActivity
- 固定 token + 授权读写 history.yml
- SnakeYAML 反序列化 → PingUtil RCE

## 解题思路
1. MainActivity 解析 expression；含 `intent:` 时缓存 Intent，计算异常则转到 BridgeActivity。
2. Bridge 校验 sha256 token 后 `startActivity` 并授予 history.yml 读写。
3. HistoryActivity 用 SnakeYAML 加载，可反序列化到 `PingUtil` 执行命令。
4. 恶意 App 写 YAML payload，把 flag 回写到 history.yml 再经 content URI 读出。

## 关键代码/payload
```yaml
!!com.qinquang.calc.PingUtil
- "127.0.0.1;cat /data/data/.../flag-*.txt > .../history.yml;"
```

## 参考链接
- https://blog.wm-team.cn/index.php/archives/87/

> 本文为对公开 writeup 的归纳总结，版权归原作者所有；请务必阅读原文核对细节。
