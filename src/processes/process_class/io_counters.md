# I/O统计

**Process.io_counters()** - [原文](https://psutil.readthedocs.io/en/latest/#psutil.Process.io_counters) <a name="Process.io_counters" ></a>

返回以命名元组形式的进程I/O分析数据，在liunx平台上可以参考 [/proc 文件系统文档][proce filesystem document]。

[proce filesystem document]: https://stackoverflow.com/questions/3633286/what-do-the-counters-in-proc-pid-io-mean "What do the counters in /proc/[pid]/io mean?"

- `read_count`: 执行的读取操作数（累计）。 这应该计算的是与读取相关的系统调用的数量，例如 UNIX 上的 `read()` 和 `pread()`。
- `write_count`: 执行的写入操作数（累计）。 这应该计算的是与写入相关的系统调用的数量，例如 UNIX 上的 `write()` 和 `pwrite()`。
- `read_bytes`: 读取的字节数（累计）。 在 BSD 上总是 -1。
- `write_bytes`: 写入的字节数（累计）。 在 BSD 上总是 -1。
  
特定于 Linux:

- `read_chars` (Linux): 此进程传递给 `read()` 和 `pread()` 系统调用的字节数（累积）。与 `read_bytes` 不同，它不关心是否发生了实际的物理磁盘 I/O。
- `write_chars` (Linux): 此进程传递给 `write()` 和 `pwrite()` 系统调用的字节数（累积）。与 `write_bytes` 不同，它不关心是否发生了实际的物理磁盘 I/O。

特定于 Windows :

- `other_count` (Windows): 除读取和写入操作外执行的 I/O 操作数。
- `other_bytes` (Windows): 在读取和写入操作以外的操作期间传输的字节数。

```python
>>> import psutil
>>> p = psutil.Process()
>>> p.io_counters()
pio(read_count=454556, write_count=3456, read_bytes=110592, write_bytes=0, read_chars=769931, write_chars=203)
```

*可用平台: Linux, BSD, Windows, AIX.*

*5.2.0 版本中修改: 在 Linux 平台增加 **read_chars** 和 **write_chars** 字段; 在 Windows 平台增加 **other_count** 和 **other_bytes** 字段.*
