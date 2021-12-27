# 进程ID列表

**psutil.pids()** - [原文](https://psutil.readthedocs.io/en/latest/#psutil.pids) <a name="psutil.pids"></a>

返回当前正在运行的**进程ID**(PID)的排序列表。 迭代所有进程并避免竞争条件 [process_iter()] 应该是首选。

```python
>>> import psutil
>>> psutil.pids()
[1, 2, 3, 5, 7, 8, 9, 10, 11, 12, 13, 14, 15, 17, 18, 19, ..., 32498]
```

*5.6.0 版本中修改: PIDs 排序后返回。*
