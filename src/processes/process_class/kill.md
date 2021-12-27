# 杀死进程

{{#include ../../links.md}}

**Process.kill()** - [原文](https://psutil.readthedocs.io/en/latest/#psutil.Process.kill) <a name="Process.kill" ></a>

通过使用 SIGKILL 信号抢先检查 PID 是否已被重用来杀死当前进程。 在 UNIX 上，这与 `os.kill(pid, signal.SIGKILL)` 相同。 在 Windows 上，这是通过使用 [TerminateProcess][win.TerminateProcess] 来完成的。 另请参阅如何[终止进程树]和[终止子进程]。
