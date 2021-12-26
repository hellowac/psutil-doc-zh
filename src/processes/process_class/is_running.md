# 是否正在运行

**Process.is_running()** - [原文](https://psutil.readthedocs.io/en/latest/#psutil.Process.is_running) <a name="Process.is_running" ></a>

返回当前进程是否在当前进程列表中运行。 这在进程消失并且它的 PID 被另一个进程重用的情况下也是可靠的，因此它优于执行 `psutil.pid_exists(p.pid)`。

**注释**: 如果进程是僵尸进程（`p.status() == psutil.STATUS_ZOMBIE`），这也将返回 `True`。