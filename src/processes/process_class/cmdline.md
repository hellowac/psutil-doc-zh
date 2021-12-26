# 执行命令行

**Process.cmdline()** - [原文](https://psutil.readthedocs.io/en/latest/#psutil.Process.cmdline) <a name="Process.cmdline" ></a>

此进程的作为字符串列表的命令号调用。 由于进程的命令行可能会更改，因此不会缓存返回值。

```python
>>> import psutil
>>> psutil.Process().cmdline()
['python', 'manage.py', 'runserver']
```
