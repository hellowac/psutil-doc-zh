# 父进程

{{#include ../../links.md}}

**Process.parent()** - [原文](https://psutil.readthedocs.io/en/latest/#psutil.Process.parent) <a name="Process.parent" ></a>

将父进程作为 [Process] 对象返回的实例方法，抢先检查 PID 是否已被重用。 如果没有已知的父 PID，则返回 `None` 。 另请参见 [ppid()] 和 [parents()] 方法。
