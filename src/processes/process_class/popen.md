# 进程管道

{{#include ../../links.md}}

**`class` psutil.Popen(\*args, \*\*kwargs)** - [原文](https://psutil.readthedocs.io/en/latest/#psutil.Popen) <a name="Popen" ></a>

与 [subprocess.Popen][subprocess.Popen] 相同，但此外它还在单个类中提供所有 [psutil.Process][Process] 的方法。 对于以下两个类共有的方法，psutil 的实现更优先：[send_signal()]、[terminate()]、[kill()]。 这样做是为了避免在其 `PID` 被重用的情况下杀死另一个进程，修复了 [BPO-6973]。

```python
>>> import psutil
>>> from subprocess import PIPE
>>>
>>> p = psutil.Popen(["/usr/bin/python", "-c", "print('hello')"], stdout=PIPE)
>>> p.name()
'python'
>>> p.username()
'giampaolo'
>>> p.communicate()
('hello\n', None)
>>> p.wait(timeout=2)
0
>>>
```

*版本 4.4.0 中改变: 新增支持上下文管理.*
