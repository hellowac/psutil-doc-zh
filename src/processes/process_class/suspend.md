# 暂停进程

**Process.suspend()** - [原文](https://psutil.readthedocs.io/en/latest/#psutil.Process.suspend) <a name="Process.suspend" ></a>

使用 ***SIGSTOP*** 信号暂停进程执行抢先检查 PID 是否已被重用。 在 UNIX 上，这与 `os.kill(pid, signal.SIGSTOP)` 相同。 在 Windows 上，这是通过暂停所有进程线程执行来完成的。
