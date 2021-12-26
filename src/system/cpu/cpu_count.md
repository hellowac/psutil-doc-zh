# 核心数量

**psutil.cpu_count(logical=True)** - [原文](https://psutil.readthedocs.io/en/latest/#psutil.cpu_count) <a name="psutil.cpu_count"></a>

返回系统中逻辑 CPU 的数量（与 Python 3.4 中的 [os.cpu_count][os.cpu_count] 相同）或 `None` 如果未确定。“逻辑 CPU”是指物理内核数乘以每个内核上可以运行的线程数（这称为超线程）。如果 **_logical_** 为 False，则仅返回物理内核的数量，如果未确定，则返回 `None`。 在 OpenBSD 和 NetBSD 上 `psutil.cpu_count(logical=False)` 总是返回 `None` 。下面是具有 2 个内核 + 超线程的系统示例:

[os.cpu_count]: https://docs.python.org/3/library/os.html#os.cpu_count "os.cpu_count"

```python
>>> import psutil
>>> psutil.cpu_count()
4
>>> psutil.cpu_count(logical=False)
2
```

请注意， `psutil.cpu_count()` 可能不一定等于当前进程可以使用的实际 CPU 数量。如果进程 CPU 亲和性已更改、正在使用 Linux cgroups 或（在 Windows 的情况下）在使用处理器组或具有超过 64 个 CPU 的系统上，这可能会有所不同。 可用 CPU 的数量可以通过以下方式获得：

```python
>>> len(psutil.Process().cpu_affinity())
1
psutil.cpu_stats()
```
