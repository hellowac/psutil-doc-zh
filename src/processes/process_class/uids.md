# 用户ID

**Process.uids()** - [原文](https://psutil.readthedocs.io/en/latest/#psutil.Process.uids) <a name="Process.uids" ></a>

返回一个由 (ruid, euid, suid) 所组成的元组，分别表示当前进程的真实用户ID，有效用户ID和暂存用户ID。这与 [os.getresuid][os.getresuid] 相同，但可用于任何进程 PID。

[os.getresuid]: https://docs.python.org/zh-cn/3/library/os.html#os.getresuid "os.getresuid"

译注例子:

```python
>>> psutil.Process().uids()
puids(real=501, effective=501, saved=501)
```

*可用平台: UNIX。*
