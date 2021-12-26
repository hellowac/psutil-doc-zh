# cpu利用率

**Process.cpu_percent(interval=None)** - [原文](https://psutil.readthedocs.io/en/latest/#psutil.Process.cpu_percent) <a name="Process.cpu_percent" ></a>

返回一个浮点数，以百分比形式表示进程 CPU 利用率，如果进程在不同 CPU 上运行多个线程，则该值也可以 `> 100.0`。当间隔 `> 0.0` 时，将处理时间与间隔（阻塞）前后经过的系统 CPU 时间进行比较。当间隔为 `0.0` 或 `None` 时，将进程时间与自上次调用以来经过的系统 CPU 时间进行比较，立即返回。这意味着第一次调用它时，它会返回一个应该忽略的无意义的 `0.0` 值。在这种情况下，为了准确起见，建议在两次调用之间至少间隔 `0.1` 秒再次调用此函数。

例子:

```python
>>> import psutil
>>> p = psutil.Process()
>>> # blocking
>>> p.cpu_percent(interval=1)
2.0
>>> # non-blocking (percentage since last call)
>>> p.cpu_percent(interval=None)
2.9
```

`注意`: *如果进程在不同 CPU 内核上运行多个线程，则返回值可以 `> 100.0`。*

`注意`: 返回的值在所有可用 CPU 之间明确没有平均分配（与 [psutil.cpu_percent()](#psutil.cpu_percent) 不同）。 这意味着在具有 2 个逻辑 CPU 的系统上运行的繁忙循环进程将被报告为具有 100% 的 CPU 利用率而不是 50%。 这样做是为了与顶级(***top***) UNIX 实例程序保持一致，并且更容易识别独立于 CPU 数量而占用 CPU 资源的进程。 必须注意的是，Windows 上的 `taskmgr.exe` 不会像这样运行（它会报告 50% 的使用率）。 要模拟 Windows `taskmgr.exe` 行为，可以执行以下操作：`p.cpu_percent() / psutil.cpu_count()`。

`警告`: 第一次使用 `interval = 0.0` 或 `None` 调用此方法时，它将返回一个无意义的 `0.0` 值，应该忽略该值。