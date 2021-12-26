# 负载信息

**psutil.getloadavg()** - [原文](https://psutil.readthedocs.io/en/latest/#psutil.getloadavg)

以元组形式返回过去 1、5 和 15 分钟的平均系统负载。“负载”表示处于可运行状态的进程，要么使用 CPU，要么等待使用 CPU（例如，等待磁盘 I/O）。在 UNIX 系统上，这依赖于 [os.getloadavg][os.getloadavg]。在 Windows 上，这是通过使用 Windows API 来模拟的，该 API 产生一个线程，该线程保持在后台运行并每 5 秒更新一次结果，模仿 UNIX 行为。因此，在 Windows 上，第一次调用它，在接下来的 5 秒内，它将返回一个无意义的 (`0.0, 0.0, 0.0`) 元组。返回的数字仅在与系统上安装的 CPU 内核数相关时才有意义。 因此，例如，具有 10 个逻辑 CPU 的系统上的值 3.14 意味着系统负载在过去 N 分钟内为 31.4%。

[os.getloadavg]: https://docs.python.org/zh-cn/3/library/os.html#os.getloadavg "获得平均负载"

```python
>>> import psutil
>>> psutil.getloadavg()
(3.14, 3.89, 4.67)
>>> psutil.cpu_count()
10
>>> # percentage representation
>>> [x / psutil.cpu_count() * 100 for x in psutil.getloadavg()]
[31.4, 38.9, 46.7]
```

可用平台: Unix, Windows

_5.6.2 版本中新增。_