# 父进程

**Process.parent()** - [原文](https://psutil.readthedocs.io/en/latest/#psutil.Process.parent) <a name="Process.parent" ></a>

将父进程作为 [Process](#psutil.Process) 对象返回的实例方法，抢先检查 PID 是否已被重用。 如果没有已知的父 PID，则返回 `None` 。 另请参见 [ppid()](#Process.ppid) 和 [parents()](#Process.parents) 方法。
