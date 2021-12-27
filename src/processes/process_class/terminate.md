# 终止进程

{{#include ../../links.md}}

**Process.terminate()** - [原文](https://psutil.readthedocs.io/en/latest/#psutil.Process.terminate) <a name="Process.terminate" ></a>

使用 SIGTERM 信号预先检查 PID 是否已被重用终止进程。 在 UNIX 上，这与 `os.kill(pid, signal.SIGTERM)` 相同。 在 Windows 上，这是 [kill()] 的别名。 另请参阅如何[终止进程树]和[终止子进程]。
