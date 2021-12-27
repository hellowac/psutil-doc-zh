# I/O优先级

{{#include ../../links.md}}

**Process.ionice(ioclass=None, value=None)** - [原文](https://psutil.readthedocs.io/en/latest/#psutil.Process.ionice) <a name="Process.ionice" ></a>

获取或设置进程的I/O良好度(优先级)。如果没有提供参数，它作为一个 get，在 Linux 上返回一个 `(ioclass, value)` 元组，在 Windows 上返回一个 ***ioclass*** 整数。如果提供了 ***ioclass*** ，它将作为一个集合。 在这种情况下，只能在 Linux 上指定一个附加值(***value***)，以便进一步提高或降低 I/O 优先级。下面是与平台相关的 ***ioclass*** 值。

Linux (参阅 [ioprio_get]手册):

- `IOPRIO_CLASS_RT`: (高) 该进程每次都首先访问磁盘。 小心使用它，因为它会使整个系统挨饿。 可以指定额外的优先级，范围从 `0`（最高）到 `7`（最低）。
- `IOPRIO_CLASS_BE`: (一般) 未设置特定 I/O 优先级的任何进程的默认值。 附加优先级范围从 `0`（最高）到 `7`（最低）。
- `IOPRIO_CLASS_IDLE`: (低) 在没有其他人需要磁盘时获取 I/O 时间。 不接受任何附加价值。
- `IOPRIO_CLASS_NONE`: 先前未设置优先级时返回。

Windows:

- `IOPRIO_HIGH`: 最高优先级.
- `IOPRIO_NORMAL`: 默认优先级.
- `IOPRIO_LOW`: 低优先级.
- `IOPRIO_VERYLOW`: 最低优先级.

下面是一个关于如何根据使用的平台设置最高 I/O 优先级的示例：

```python
>>> import psutil
>>> p = psutil.Process()
>>> if psutil.LINUX:
...     p.ionice(psutil.IOPRIO_CLASS_RT, value=7)
... else:
...     p.ionice(psutil.IOPRIO_HIGH)
...
>>> p.ionice()  # get
pionice(ioclass=<IOPriority.IOPRIO_CLASS_RT: 1>, value=7)
```

*可用平台: Linux, Windows Vista+ 。*

*5.6.2 版本中修改: Windows 接受新的 `IOPRIO_*` 常量，包括新的 `IOPRIO_HIGH`。*
