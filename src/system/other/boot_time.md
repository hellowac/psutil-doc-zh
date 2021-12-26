# 启动时间

**psutil.boot_time()** - [原文](https://psutil.readthedocs.io/en/latest/#psutil.boot_time)

返回自纪元(epoch)以来以秒表示的系统启动时间。 例子：

```python
>>> import psutil, datetime
>>> psutil.boot_time()
1389563460.0
>>> datetime.datetime.fromtimestamp(psutil.boot_time()).strftime("%Y-%m-%d %H:%M:%S")
'2014-01-12 22:51:00'
```

**注释**: 在 Windows 上，如果它在不同的进程中使用，这个函数可能会返回一个减少(off by) 1 秒的时间（参阅[问题 #1007][issue#1007]）。

[issue#1007]: https://github.com/giampaolo/psutil/issues/1007 "issue #1007"