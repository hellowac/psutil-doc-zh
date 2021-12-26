# 运行内存

**psutil.virtual_memory()** - [原文](https://psutil.readthedocs.io/en/latest/#psutil.virtual_memory)

以包含以下字段的命名元组形式返回有关系统内存使用情况的统计信息，以**字节**为单位。 主要指标：

- `total`: 总物理内存（独占交换）。
- `available`: 可以立即分配给进程而无需系统进行交换的内存。这是通过根据平台对不同的内存值求和来计算的，它应该用于以跨平台方式监控实际内存使用情况。

其他指标:

- `used`: 使用的内存，计算方式因平台而异，仅供参考。 **total - free** 不一定匹配 **used**。
- `free`: 根本没有使用（归零）的随时可用的内存； 请注意，这并不反映实际可用内存（请改用可用(`available`)内存）。 **total - used** 不一定匹配 **free**。
- `active` (UNIX): 当前正在使用或最近使用的内存，因此它在 RAM 中。
- `inactive` (UNIX): 标记为未使用的内存。
- `buffers` (Linux, BSD): 缓存文件系统元数据等内容。
- `cached` (Linux, BSD): 缓存各种东西。
- `shared` (Linux, BSD): 可以被多个进程同时访问的内存。
- `slab` (Linux): 内核数据结构缓存。
- `wired` (BSD, macOS): 标记为始终保留在 RAM 中的内存。 它永远不会移动到磁盘。

已用(`used`)和可用(`available`)的总和不一定等于总数(`total`)。 在 Windows 上可用(`available`)和免费(`free`)是一样的。 请参阅 [meminfo.py][meminfo.py] 脚本并提供了有关如何以可读形式**转换字节**的示例。

[meminfo.py]: https://github.com/giampaolo/psutil/blob/master/scripts/meminfo.py "meminfo.py"

**注意**: 如果您只想知道跨平台方式还剩下多少物理内存，只需依赖可用(`available`)字段即可。

```python
>>> import psutil
>>> mem = psutil.virtual_memory()
>>> mem
svmem(total=10367352832, available=6472179712, percent=37.6, used=8186245120, free=2181107712, active=4748992512, inactive=2758115328, buffers=790724608, cached=3500347392, shared=787554304, slab=199348224)
>>>
>>> THRESHOLD = 100 * 1024 * 1024  # 100MB
>>> if mem.available <= THRESHOLD:
...     print("warning")
...
>>>
```

_4.2.0 版本中修改: 在Linux中新增了 `shared` 指标。_

_5.4.4 版本中修改: 在Linux中新增了 `slab` 指标。_