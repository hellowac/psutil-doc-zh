# 利用率

**psutil.disk_usage(path)** - [原文](https://psutil.readthedocs.io/en/latest/#psutil.disk_usage)

返回有关包含给定路径的分区的磁盘使用统计信息作为命名元组，包括以字节表示的总空间(**total**)、已用空间(**used**)和可用空间(**free**)，以及使用百分比(**percentage** usage)。如果路径(**_path_**)不存在，则引发 `OSError`。 从 Python 3.3 开始，这也可以作为 [shutil.disk_usage][shutil.disk_usage] 使用（参见 [BPO-12442][BPO-12442]）。 请参阅提供示例用法的 [disk_usage.py][disk_usage.py] 脚本。

[shutil.disk_usage]: https://docs.python.org/zh-cn/3/library/shutil.html#shutil.disk_usage. "shutil.disk_usage"
[BPO-12442]: https://bugs.python.org/issue12442 "BPO-12442"

```python
>>> import psutil
>>> psutil.disk_usage('/')
sdiskusage(total=21378641920, used=4809781248, free=15482871808, percent=22.5)
```

**注意**: UNIX 通常为 root 用户保留 5% 的总磁盘空间。UNIX 上的 **_total_** 和 **_used_** 字段是指总空间和已用空间，而 **_free_** 表示用户可用的空间，**_percent_** 表示用户利用率（参见[源代码][source-code]）。这就是为什么百分比(**_percent_**)值可能看起来比您预期的大 5%。 另请注意，这 4 个值都与“`df`” 命令行程序一致的。

[source-code]: https://github.com/giampaolo/psutil/blob/3dea30d583b8c1275057edb1b3b720813b4d0f60/psutil/_psposix.py#L123 "source-code"

_4.3.0 版本中修改: 百分比(**percent**)值考虑了`root`保留空间。_