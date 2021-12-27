# 利用率详细

[cpu_percent()]: cpu_percent.md
[psutil.cpu_times(percpu=True)]: cpu_times.md

**psutil.cpu_times_percent(interval=None, percpu=False)** - [原文](https://psutil.readthedocs.io/en/latest/#psutil.cpu_times_percent)

就像 [cpu_percent()] ，但提供 [psutil.cpu_times(percpu=True)] 返回的每个 CPU 的**_时间利用率百分比。interval_** 和 **_percpu_** 参数的含义与 [cpu_percent()] 中的含义相同。 在 Linux 上，“**guest**”和“**guest\_nice**”百分比不计入“**user**”和“**user\_nice**”百分比。

**⚠️警告**: 第一次使用 **_interval_** = `0.0` 或 `None` 调用此函数时，它将返回一个无意义的 `0.0` 值，应该忽略该值。

_4.1.0 版本中更新_: 对于Windows平台返回值将包含两个新字段 `interrupt` 和 `dpc` 。
