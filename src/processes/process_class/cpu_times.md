# cpu时间

{{#include ../../links.md}}

**Process.cpu_times()** - [原文](https://psutil.readthedocs.io/en/latest/#psutil.Process.cpu_times) <a name="Process.cpu_times" ></a>

Return a named tuple representing the accumulated process times, in seconds (see explanation). This is similar to os.times but can be used for any process PID.

返回一个命名元组，表示累计处理时间，以秒为单位（见[解释](http://stackoverflow.com/questions/556405/)）。 这类似于 [os.times] 但可用于任何进程 PID。

- `user`: 在用户模式下花费的时间。
- `system`: 在内核模式中花费的时间。
- `children_user`: 所有子进程的用户时间（在 Windows 和 macOS 上始终为 0）。
- `children_system`: 所有子进程的系统时间（在 Windows 和 macOS 上始终为 0）。
- `iowait`: (Linux) 等待阻塞 I/O 完成所花费的时间。 这个值被排除在用户和系统时间计数之外（因为 CPU 没有做任何工作）。

```python
>>> import psutil
>>> p = psutil.Process()
>>> p.cpu_times()
pcputimes(user=0.03, system=0.67, children_user=0.0, children_system=0.0, iowait=0.08)
>>> sum(p.cpu_times()[:2])  # cumulative, excluding children and iowait
0.70
```

*4.1.0 版本中修改: 返回两个额外的字段：**children_user** 和 **children_system** 。*

*5.6.4 版本中修改: 在 Linux 上添加了 **iowait** 字段。*
