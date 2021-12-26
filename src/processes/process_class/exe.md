# 可执行文件绝对路径

**Process.exe()** - [原文](https://psutil.readthedocs.io/en/latest/#psutil.Process.exe) <a name="Process.exe" ></a>

进程的可执行文件绝对路径。 在某些系统上，这也可能是一个空字符串。 返回值在第一次调用后被缓存。

```python
>>> import psutil
>>> psutil.Process().exe()
'/usr/bin/python2.7'
```
