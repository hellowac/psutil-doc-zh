# 字典信息

**Process.as_dict(attrs=None, ad_value=None)** - [原文](https://psutil.readthedocs.io/en/latest/#psutil.Process.as_dict) <a name="Process.as_dict" ></a>

以字典形式检索进程的多个信息的实例方法。如果指定了 ***attrs*** ，则它必须是反映 [Process](#psutil.Process) 类可用的属性名称的字符串列表。以下是可能的字符串值列表：`'cmdline'`, `'connections'`, `'cpu_affinity'`, `'cpu_num'`, `'cpu_percent'`, `'cpu_times'`, `'create_time'`, `'cwd'`, `'environ'`, `'exe'`, `'gids'`, `'io_counters'`, `'ionice'`, `'memory_full_info'`, `'memory_info'`, `'memory_maps'`, `'memory_percent'`, `'name'`, `'nice'`, `'num_ctx_switches'`, `'num_fds'`, `'num_handles'`, `'num_threads'`, `'open_files'`, `'pid'`, `'ppid'`, `'status'`, `'terminal'`, `'threads'`, `'uids'`, `'username'`. 如果没有传递 ***attrs*** 参数，则假定为所有公共的只读属性。***ad_value*** 是分配给字典键的值，以防在检索该特定进程信息时引发 [AccessDenied](#psutil.AccessDenied) 或 [ZombieProcess](#psutil.ZombieProcess) 异常。 在内部， [as_dict()](#Process.as_dict) 使用 [oneshot()](#Process.oneshot) 上下文管理器，因此也无需使用它。

```python
>>> import psutil
>>> p = psutil.Process()
>>> p.as_dict(attrs=['pid', 'name', 'username'])
{'username': 'giampaolo', 'pid': 12366, 'name': 'python'}
>>>
>>> # get a list of valid attrs names
>>> list(psutil.Process().as_dict().keys())
['status', 'cpu_num', 'num_ctx_switches', 'pid', 'memory_full_info', 
 'connections', 'cmdline', 'create_time', 'ionice', 'num_fds', 
 'memory_maps', 'cpu_percent', 'terminal', 'ppid', 'cwd', 'nice', 
 'username', 'cpu_times', 'io_counters', 'memory_info', 'threads', 
 'open_files', 'name', 'num_threads', 'exe', 'uids', 'gids', 
 'cpu_affinity', 'memory_percent', 'environ']
```

*3.0.0 版本中修改: **ad_value** 在引发 [ZombieProcess](#psutil.ZombieProcess) 异常时也使用，不仅是 [AccessDenied](#psutil.AccessDenied)。*

*4.5.0 版本中修改: 由于 [oneshot()](#Process.oneshot) 上下文管理器，[as_dict()](#Process.as_dict) 的速度要快得多。*
