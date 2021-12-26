# 用户

**psutil.users()** - [原文](https://psutil.readthedocs.io/en/latest/#psutil.users)

将当前连接在系统上的用户作为命名元组列表返回，包括以下字段：

- `name`: 用户名.
- `terminal`: 与用户关联的 `tty` 或 `伪tty` ，如果有，否则为 `None` 。
- `host`: 与条目关联的主机名（如果有）。
- `started`: 创建时间作为一个浮点数，以自纪元（epoch）以来的秒数表示。
- `pid`: 登录进程的 PID（如 sshd、tmux、gdm-session-worker 等）。 在 Windows 和 OpenBSD 上，PID 始终为 `None` 。

例子:

```python
>>> import psutil
>>> psutil.users()
[suser(name='giampaolo', terminal='pts/2', host='localhost', started=1340737536.0, pid=1352),
 suser(name='giampaolo', terminal='pts/3', host='localhost', started=1340737792.0, pid=1788)]
```

5.3.0 版本中修改: added “pid” field