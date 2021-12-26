# 利用率

**psutil.cpu_percent(interval=None, percpu=False)** - [原文](https://psutil.readthedocs.io/en/latest/#psutil.cpu_percent) <a name="psutil.cpu_percent"></a>

返回一个浮点数，以百分比形式表示当前系统范围内的 CPU 利用率。 当间隔 > `0.0` 时比较间隔前后经过的系统 CPU 时间（阻塞）。 当间隔为 `0.0` 或 `None` 时，比较自上次调用或模块导入以来经过的系统 CPU 时间，立即返回。这意味着第一次调用它时，它会返回一个你应该忽略的无意义的 `0.0` 值。在这种情况下，为了准确起见，建议在两次调用之间至少间隔 `0.1` 秒来调用此函数。当 **_percpu_** 为 `True` 时，返回一个浮点数列表，以百分比形式表示每个 CPU 的利用率。 列表的第一个元素指的是第一个 CPU，第二个元素指的是第二个 CPU，依此类推。列表的顺序在调用之间是一致的。

```python
>>> import psutil
>>> # blocking
>>> psutil.cpu_percent(interval=1)
2.0
>>> # non-blocking (percentage since last call)
>>> psutil.cpu_percent(interval=None)
2.9
>>> # blocking, per-cpu
>>> psutil.cpu_percent(interval=1, percpu=True)
[2.0, 1.0]
>>>
```

**⚠️警告**: 第一次使用 **_interval_** = `0.0` 或 `None` 调用此函数时，它将返回一个无意义的 `0.0` 值，您应该忽略该值。