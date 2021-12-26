# IO统计

**psutil.disk_io_counters(perdisk=False, nowrap=True)** - [原文](https://psutil.readthedocs.io/en/latest/#psutil.disk_io_counters)

将系统范围的磁盘 I/O 统计信息作为命名元组返回，包括以下字段：

- `read_count`: 读取次数
- `write_count`: 写入次数
- `read_bytes`: 读取的字节数
- `write_bytes`: 写入的字节数

特定于平台的字段:

- `read_time`(除了 NetBSD 和 OpenBSD): 从磁盘读取所花费的时间（以毫秒为单位）
- `write_time`(除了 NetBSD 和 OpenBSD): 写入磁盘所花费的时间（以毫秒为单位）
- `busy_time`(Linux, FreeBSD):  花费在实际 I/O 上的时间（以毫秒为单位）
- `read_merged_count` (Linux): 合并读取的数量（参见 [iostats][iostats] 文档）
- `write_merged_count` (Linux): 合并写入的数量（请参阅 [iostats][iostats] 文档）

[iostats]: https://www.kernel.org/doc/Documentation/iostats.txt "iostats"

如果 **_perdisk_** 为 `True` ，则将系统上安装的每个物理磁盘的相同信息作为字典返回，分区名称作为键，上面描述的命名元组作为值。有关示例应用程序，参见 [iotoop.py][iotoop.py]。在某些系统（例如 Linux）上，在非常繁忙或寿命很长的系统上，内核返回的数字可能会溢出并换行（从零开始）。如果 **_nowrap_** 为 `True`，psutil 将在函数调用中检测并调整这些数字，并将“旧值”添加到“新值”，以便返回的数字始终增加或保持不变，但永远不会减少。`disk_io_counters.cache_clear()` 可用于使 **_nowrap_** 缓存无效。 在 Windows 上，可能需要首先从 cmd.exe 发出 `diskperf -y` 命令以启用 IO 计数器。 在无盘机器上，如果 **_perdisk_** 为 `True`，此函数将返回 `None` 或 `{}`。

[iotoop.py]: https://github.com/giampaolo/psutil/blob/master/scripts/iotop.py "io top"

```python
>>> import psutil
>>> psutil.disk_io_counters()
sdiskio(read_count=8141, write_count=2431, read_bytes=290203, write_bytes=537676, read_time=5868, write_time=94922)
>>>
>>> psutil.disk_io_counters(perdisk=True)
{'sda1': sdiskio(read_count=920, write_count=1, read_bytes=2933248, write_bytes=512, read_time=6016, write_time=4),
 'sda2': sdiskio(read_count=18707, write_count=8830, read_bytes=6060, write_bytes=3443, read_time=24585, write_time=1572),
 'sdb1': sdiskio(read_count=161, write_count=0, read_bytes=786432, write_bytes=0, read_time=44, write_time=0)}
```

**注意**: 在 Windows 上，可能需要先执行“`diskperf -y`”命令，否则该函数将找不到任何磁盘。

_5.3.0 版本中修改: 由于新的 nowrap 参数，数字不再在调用之间换行（从零开始）。_

_4.0.0 版本中修改: 添加了 **busy_time**(Linux, FreeBSD),**read_merged_count**和**write_merged_count** (Linux) 字段。_

_4.0.0 版本中修改: NetBSD 不再有 **read_time**和**write_time** 字段。_