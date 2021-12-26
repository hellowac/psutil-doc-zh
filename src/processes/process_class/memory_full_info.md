# 内存完全信息

**Process.memory_full_info()** - [原文](https://psutil.readthedocs.io/en/latest/#psutil.Process.memory_full_info) <a name="Process.memory_full_info" ></a>

此方法返回与 [memory_info()](#Process.memory_info) 相同的信息，此外，在某些平台（Linux、macOS、Windows）上，还提供额外的指标（`USS`、`PSS` 和 `swap` ）。附加指标更好地表示了“有效”进程内存消耗（在 USS 的情况下），如[本博文][blog-post]中详细解释的那样。它通过传递整个进程地址来实现。因此，它通常需要比 [memory_info()](#Process.memory_info) 更高的用户权限，并且速度要慢得多。在没有实现额外字段的平台上，这只是返回与 [memory_info()](#Process.memory_info) 相同的指标。

[blog-post]: https://gmpy.dev/blog/2016/real-process-memory-and-environ-in-python "blog post with USS"

- `uss` (Linux, macOS, Windows): 又名 “Unique Set Size”, 这是一个进程唯一的内存，如果进程现在终止，它将被释放。
- `pss` (Linux): 又名 “Proportional Set Size”, 是与其他进程共享的内存量，以在共享它的进程之间平均分配的方式计算。例如：如果一个进程拥有 10 MB 的空间，并且与另一个进程共享 10 MB，则其 PSS 将为 15 MB。
- `swap` (Linux): 已交换出到磁盘的内存量。

**注释**: *`uss` 可能是确定进程实际使用多少内存的最具代表性的指标。它表示如果进程现在终止将被释放的内存量。*

**译注**: 参考: [VSS/RSS/PSS/USS 的介绍](https://www.jianshu.com/p/3bab26d25d2e)

Linux 上的例子:

```python
>>> import psutil
>>> p = psutil.Process()
>>> p.memory_full_info()
pfullmem(rss=10199040, vms=52133888, shared=3887104, text=2867200, lib=0, data=5967872, dirty=0, uss=6545408, pss=6872064, swap=0)
>>>
```

同样参考示例脚本: [procsmem.py][procsmem.py]

[procsmem.py]: https://github.com/giampaolo/psutil/blob/master/scripts/procsmem.py "procsmem.py"

*4.0.0 版本中新增.*
