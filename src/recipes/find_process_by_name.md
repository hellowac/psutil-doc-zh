# 按名称查找进程

{{#include ../links.md}}

参考: [原文](https://psutil.readthedocs.io/en/latest/#find-process-by-name)

根据 [Process.name()] 核查字符串：

```python
import psutil

def find_procs_by_name(name):
    "Return a list of processes matching 'name'."
    ls = []
    for p in psutil.process_iter(['name']):
        if p.info['name'] == name:
            ls.append(p)
    return ls
```

更高级一点，根据 [Process.name()]、[Process.exe()] 和 [Process.cmdline()] 检查字符串：

```python
import os
import psutil

def find_procs_by_name(name):
    "Return a list of processes matching 'name'."
    ls = []
    for p in psutil.process_iter(["name", "exe", "cmdline"]):
        if name == p.info['name'] or \
                p.info['exe'] and os.path.basename(p.info['exe']) == name or \
                p.info['cmdline'] and p.info['cmdline'][0] == name:
            ls.append(p)
    return ls
```
