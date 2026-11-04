---
title: DataPulse
competition: 羊城杯
year: 2026
category: Web
tags: ['ssrf', 'gopher', 'redis', 'django-session', 'pickle']
sources: ['https://xz.aliyun.com/news/93035', 'https://xz.aliyun.com/news/93039']
---

# DataPulse

## 题目信息

- 分类：WEB（HARD）
- 栈：Django + gunicorn + Celery/Redis
- 功能：任务调度 + 可控 Webhook / retry-webhook

## 考点

- Webhook SSRF：黑名单只挡字面回环，可用 `127.1` / 十进制 IP 等绕过
- `urllib` 支持 `gopher://` → 无密码 Redis 完整 RESP
- Django cache session 为 pickle → 写恶意 session 触发 RCE；`/readflag` setuid 读 flag

## 解题思路

1. 注册登录，建任务，用 retry-webhook 探测内网（8000 自身、6379 Redis）。
2. gopher 发 Redis 命令，确认 db1 存 `:1:django.contrib.sessions.cache…`。
3. 写入协议 0/`os.system` 等**不依赖自定义类**的 pickle；带原 cookie 访问 dashboard 触发。
4. 执行 `/readflag`（直接读 `/flag.txt` 权限不足）。

## 关键代码/payload

```python
# pickle protocol0 调用 os.system（示意）
payload = b"cos\\nsystem\\n(S'/readflag'\\ntR."
# Redis: SET :1:django.contrib.sessions.cache<sid> <payload>
```

注意：自定义 `__reduce__` 类在目标 `__main__` 不存在会失败。

## 参考链接

- https://xz.aliyun.com/news/93035
- https://xz.aliyun.com/news/93039
