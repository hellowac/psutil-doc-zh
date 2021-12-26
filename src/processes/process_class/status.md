# 进程状态

**Process.status()** - [原文](https://psutil.readthedocs.io/en/latest/#psutil.Process.status) <a name="Process.status" ></a>

以字符串方式返回当前进程状态。 返回的字符串是 [psutil.STATUS_*](#process-status-constant) 常量之一。

译注例子:

```python
>>> psutil.Process().status()
'running'
```
