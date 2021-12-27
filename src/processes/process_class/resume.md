# 恢复进程

**Process.resume()** - [原文](https://psutil.readthedocs.io/en/latest/#psutil.Process.resume) <a name="Process.resume" ></a>

使用 SIGCONT 信号恢复进程执行抢先检查 PID 是否已被重用。 在 UNIX 上，这与 `os.kill(pid, signal.SIGCONT)` 相同。 在 Windows 上，这是通过恢复所有进程线程执行来完成的。
