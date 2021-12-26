# 创建时间


**Process.create_time()** - [原文](https://psutil.readthedocs.io/en/latest/#psutil.Process.create_time) <a name="Process.create_time" ></a>

进程创建时间，以自纪元以来的秒数表示的浮点数。 返回值在第一次调用后被缓存。

```python
>>> import psutil, datetime
>>> p = psutil.Process()
>>> p.create_time()
1307289803.47
>>> datetime.datetime.fromtimestamp(p.create_time()).strftime("%Y-%m-%d %H:%M:%S")
'2011-03-05 18:03:52'
```
