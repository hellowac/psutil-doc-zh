# 杀死进程

**Process.kill()** - [原文](https://psutil.readthedocs.io/en/latest/#psutil.Process.kill) <a name="Process.kill" ></a>

通过使用 SIGKILL 信号抢先检查 PID 是否已被重用来杀死当前进程。 在 UNIX 上，这与 `os.kill(pid, signal.SIGKILL)` 相同。 在 Windows 上，这是通过使用 [TerminateProcess][win.TerminateProcess] 来完成的。 另请参阅如何[终止进程树](#kill-process-tree)和[终止子进程](#kill-child-process)。

[win.TerminateProcess]: https://docs.microsoft.com/en-us/windows/desktop/api/processthreadsapi/nf-processthreadsapi-terminateprocess "WIN终止进程"