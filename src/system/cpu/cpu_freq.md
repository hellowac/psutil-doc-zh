# 频率信息

**psutil.cpu_freq(percpu=False)** - [原文](https://psutil.readthedocs.io/en/latest/#psutil.cpu_freq)

将 CPU 频率作为命名元组返回，包括以 Mhz 表示的当前、最小和最大频率。 在 Linux 中当前频率报告实时值，在所有其他平台上它代表标称的“固定”值。如果 **_percpu_** 为 `True` 并且系统支持 per-cpu 频率检索（仅限 Linux），则为每个 CPU 返回一个频率列表，如果不是，则返回一个包含单个元素的列表。如果无法确定最小值和最大值，则将它们设置为 0。

样例 (Linux):

```python
>>> import psutil
>>> psutil.cpu_freq()
scpufreq(current=931.42925, min=800.0, max=3500.0)
>>> psutil.cpu_freq(percpu=True)
[scpufreq(current=2394.945, min=800.0, max=3500.0),
 scpufreq(current=2236.812, min=800.0, max=3500.0),
 scpufreq(current=1703.609, min=800.0, max=3500.0),
 scpufreq(current=1754.289, min=800.0, max=3500.0)]
```

可用平台: Linux, macOS, Windows, FreeBSD

_5.1.0版本中新增。_

_5.5.1版本中更新：添加了 FreeBSD 支持。_