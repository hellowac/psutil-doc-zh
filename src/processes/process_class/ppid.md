# 父进程ID

{{#include ../../links.md}}

**Process.ppid()** - [原文](https://psutil.readthedocs.io/en/latest/#psutil.Process.ppid) <a name="Process.ppid" ></a>

返回父进程PID。 在 Windows 上，第一次调用后会缓存返回值。在 POSIX 类型机器上时则不会缓存，因为如果进程变成僵尸进程， ***ppid*** 可能会改变，另见 [parent()] 和 [parents()] 方法。
