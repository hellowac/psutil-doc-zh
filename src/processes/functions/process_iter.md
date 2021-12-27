# 迭代进程

{{#include ../../links.md}}

**psutil.process_iter(attrs=None, ad_value=None)** - 原文 <a name="psutil.process_iter"></a>

返回一个迭代器，为本地机器上的所有正在运行的进程产生一个 [Process] 类实例。 这应该优于 [psutil.pids()] 来迭代进程，因为它不受竞争条件的影响。

每个 [Process] 实例只创建一次，然后在下次调用 [psutil.process_iter()] 时缓存（如果 PID 仍然存在）。 它还确保进程 PID 不被重用。

***attrs*** 和 ***ad_value*** 与 [Process.as_dict()] 具有相同的含义。 如果指定了 ***attrs*** ，则 [Process.as_dict()] 结果将存储为附加到返回的 [Process] 实例的 `info` 属性。 如果 ***attrs*** 是一个空列表，它将检索所有进程信息（比较慢）。

返回进程的排序顺序基于它们的 PID。

例子:

```python
>>> import psutil
>>> for proc in psutil.process_iter(['pid', 'name', 'username']):
...     print(proc.info)
...
{'name': 'systemd', 'pid': 1, 'username': 'root'}
{'name': 'kthreadd', 'pid': 2, 'username': 'root'}
{'name': 'ksoftirqd/0', 'pid': 3, 'username': 'root'}
...
```

创建类似于 `{pid: info, ...}` 数据结构的字典：

```python
>>> import psutil
>>> procs = {p.pid: p.info for p in psutil.process_iter(['name', 'username'])}
>>> procs
{1: {'name': 'systemd', 'username': 'root'},
 2: {'name': 'kthreadd', 'username': 'root'},
 3: {'name': 'ksoftirqd/0', 'username': 'root'},
 ...}
```

*5.3.0 版本中修改: 新增 “**attrs**” 和 “**ad_value**” 参数.*
