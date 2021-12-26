# 终止进程树

参考: [原文](https://psutil.readthedocs.io/en/latest/#kill-process-tree)

```python
import os
import signal
import psutil

def kill_proc_tree(pid, sig=signal.SIGTERM, include_parent=True,
                   timeout=None, on_terminate=None):
    """Kill a process tree (including grandchildren) with signal
    "sig" and return a (gone, still_alive) tuple.
    "on_terminate", if specified, is a callback function which is
    called as soon as a child terminates.
    """
    assert pid != os.getpid(), "won't kill myself"
    parent = psutil.Process(pid)
    children = parent.children(recursive=True)
    if include_parent:
        children.append(parent)
    for p in children:
        try:
            p.send_signal(sig)
        except psutil.NoSuchProcess:
            pass
    gone, alive = psutil.wait_procs(children, timeout=timeout,
                                    callback=on_terminate)
    return (gone, alive)
```

### **过滤和排序进程** (Filtering and sorting processes)

参考: [原文](https://psutil.readthedocs.io/en/latest/#filtering-and-sorting-processes)

这个代码样例合集将展示如果通过`process_iter()`函数去过滤和排序进程。开始:

```python
>>> import psutil
>>> from pprint import pprint as pp
```

当前用户拥有的进程:

```python
>>> import getpass
>>> pp([(p.pid, p.info['name']) for p in psutil.process_iter(['name', 'username']) if p.info['username'] == getpass.getuser()])
(16832, 'bash'),
(19772, 'ssh'),
(20492, 'python')]
```

正在运行的进程:

```python
>>> pp([(p.pid, p.info) for p in psutil.process_iter(['name', 'status']) if p.info['status'] == psutil.STATUS_RUNNING])
[(1150, {'name': 'Xorg', 'status': 'running'}),
 (1776, {'name': 'unity-panel-service', 'status': 'running'}),
 (20492, {'name': 'python', 'status': 'running'})]
```

使用log日志文件的进程:

```python
>>> for p in psutil.process_iter(['name', 'open_files']):
...      for file in p.info['open_files'] or []:
...          if file.path.endswith('.log'):
...               print("%-5s %-10s %s" % (p.pid, p.info['name'][:10], file.path))
...
1510  upstart    /home/giampaolo/.cache/upstart/unity-settings-daemon.log
2174  nautilus   /home/giampaolo/.local/share/gvfs-metadata/home-ce08efac.log
2650  chrome     /home/giampaolo/.config/google-chrome/Default/data_reduction_proxy_leveldb/000003.log
```

进程消耗超过500M的内存:

```python
>>> pp([(p.pid, p.info['name'], p.info['memory_info'].rss) for p in psutil.process_iter(['name', 'memory_info']) if p.info['memory_info'].rss > 500 * 1024 * 1024])
[(2650, 'chrome', 532324352),
 (3038, 'chrome', 1120088064),
 (21915, 'sublime_text', 615407616)]
```

CPU耗时最多的前 3 个进程：

```python
>>> pp([(p.pid, p.info['name'], sum(p.info['cpu_times'])) for p in sorted(psutil.process_iter(['name', 'cpu_times']), key=lambda p: sum(p.info['cpu_times'][:2]))][-3:])
[(2721, 'chrome', 10219.73),
 (1150, 'Xorg', 11116.989999999998),
 (2650, 'chrome', 18451.97)]
```

### **字节转换** (Bytes conversion)

参考: [原文](https://psutil.readthedocs.io/en/latest/#bytes-conversion)

```python
import psutil

def bytes2human(n):
    # http://code.activestate.com/recipes/578019
    # >>> bytes2human(10000)
    # '9.8K'
    # >>> bytes2human(100001221)
    # '95.4M'
    symbols = ('K', 'M', 'G', 'T', 'P', 'E', 'Z', 'Y')
    prefix = {}
    for i, s in enumerate(symbols):
        prefix[s] = 1 << (i + 1) * 10
    for s in reversed(symbols):
        if n >= prefix[s]:
            value = float(n) / prefix[s]
            return '%.1f%s' % (value, s)
    return "%sB" % n

total = psutil.disk_usage('/').total
print(total)
print(bytes2human(total))
```

…打印:

```python
100399730688
93.5G
```

## **常见问题** (FAQs)

参考: [原文](https://psutil.readthedocs.io/en/latest/#faqs)

- Q: 为什么某些进程我会无权限?
- A: 当你查询其他用户拥有的进程时可能会发生这种情况，尤其是在 macOS (参考[问题 #883](https://github.com/giampaolo/psutil/issues/883)) 和 Windows 上。不幸的是，除了以更高的权限运行 Python 进程之外，对此无能为力。 在 Unix 上，你可以以 root 身份运行 Python 进程或使用 SUID 位（ps 和 netstat 执行此操作）。 在 Windows 上，你可以将 Python 进程作为 NT AUTHORITY\SYSTEM 运行，或者将 Python 脚本安装为 Windows 服务（ProcessHacker 执行此操作）。
- Q: 支持在windows系统的MinGW上运行吗?
- A: 不支持, 你应该使用 Visual Studio (参阅 [开发指南](https://github.com/giampaolo/psutil/blob/master/docs/DEVGUIDE.rst)).

## **测试** (Running tests)

参考: [原文](https://psutil.readthedocs.io/en/latest/#running-tests)

```python
python3 -m psutil.tests
```
