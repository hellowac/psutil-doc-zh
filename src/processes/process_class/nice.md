# 优先级

{{#include ../../links.md}}

**Process.nice(value=None)** - [原文](https://psutil.readthedocs.io/en/latest/#psutil.Process.nice) <a name="Process.nice" ></a>

获取或设置进程良好度（优先级）。 在 UNIX 上，这是一个数字，通常从 `-20` 到 `20` 。nice 值越高，进程的优先级越低。

```python
>>> import psutil
>>> p = psutil.Process()
>>> p.nice(10)  # set
>>> p.nice()  # get
10
>>>
```

从 Python 3.3 开始，此功能类似于 [os.getpriority] 和 [os.setpriority]（参见 [BPO-10784]）。 在 Windows 上，这是通过 Windows API 的 [GetPriorityClass] 和 [SetPriorityClass] 实现的，***value*** 是 [psutil.*_PRIORITY_CLASS] 常量之一， 对应于MSDN文档。 在 Windows 上增加进程优先级的示例如下：

```python
>>> p.nice(psutil.HIGH_PRIORITY_CLASS)
```
