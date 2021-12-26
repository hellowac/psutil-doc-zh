# 检查进程是否存在

**psutil.pid_exists(pid)** - [原文](https://psutil.readthedocs.io/en/latest/#psutil.pid_exists)

检查给定的 PID 是否存在于当前进程列表中。 这比执行 `pid in psutil.pids()` 更快，应该是首选。
