# 快照

**Process.oneshot()** - [原文](https://psutil.readthedocs.io/en/latest/#psutil.Process.oneshot) <a name="Process.oneshot" ></a>
  
实例的上下文管理器可显著加快同时检索多个进程信息的速度。内部不同的进程信息（例如 [name()](#Process.name), [ppid()](#Process.ppid), [uids()](#Process.uids), [create_time()](#Process.create_time), ...）可以通过使用相同的例程获取，但只返回一个值，其他值被丢弃。当使用上下文管理器时，内部只执行一次（在下面的 [name()](#Process.name) 示例中），返回感兴趣的值并缓存其他值。共享相同内部例程的后续调用将返回缓存值。 退出上下文管理器块时清除缓存。建议是每次检索有关该进程的多个信息时都使用此方法。 如果很幸运，获取值将会得到极大的加速。 例子：

```python
>>> import psutil
>>> p = psutil.Process()
>>> with p.oneshot():
...     p.name()  # execute internal routine once collecting multiple info
...     p.cpu_times()  # return cached value
...     p.cpu_percent()  # return cached value
...     p.create_time()  # return cached value
...     p.ppid()  # return cached value
...     p.status()  # return cached value
...
>>>
```

以下是可以利用加速的方法列表，具体取决于使用的平台。在下表中，垂直列表示哪些进程方法可以在某个平台内调用时内部有效地组合在一起。最后一行 (speedup) 显示了将所有方法一起调用时可以获得的加速比的近似值（最佳情况）。

**译注**: 原文说的是 “horizontal emtpy rows” 水平空行，但根据表格实际内容，应为某个平台对应的垂直列，并且原文的 “The last column” 应该是指最后一行。

| **Linux**                                       | **Windows**                                     | **macOS**                                       | **BSD**                                         | **SunOS**                                   | **AIX**                                     |
| ----------------------------------------------- | ----------------------------------------------- | ----------------------------------------------- | ----------------------------------------------- | ------------------------------------------- | ------------------------------------------- |
| [cpu_num()](#Process.cpu_num)                   | [cpu_percent()](#Process.cpu_percent)           | [cpu_percent()](#Process.cpu_percent)           | [cpu_num()](#Process.cpu_num)                   | [name()](#Process.name)                     | [name()](#Process.name)                     |
| [cpu_percent()](#Process.cpu_percent)           | [cpu_times()](#Process.cpu_times)               | [cpu_times()](#Process.cpu_times)               | [cpu_percent()](#Process.cpu_percent)           | [cmdline()](#Process.cmdline)               | [cmdline()](#Process.cmdline)               |
| [cpu_times()](#Process.cpu_times)               | [io_counters()](#Process.io_counters)           | [memory_info()](#Process.memory_info)           | [cpu_times()](#Process.cpu_times)               | [create_time()](#Process.create_time)       | [create_time()](#Process.create_time)       |
| [create_time()](#Process.create_time)           | [memory_info()](#Process.memory_info)           | [memory_percent()](#Process.memory_percent)     | [create_time()](#Process.create_time)           | -                                           | -                                           |
| [name()](#Process.name)                         | [memory_maps()](#Process.memory_maps)           | [num_ctx_switches()](#Process.num_ctx_switches) | [gids()](#Process.gids)                         | [memory_info()](#Process.memory_info)       | [memory_info()](#Process.memory_info)       |
| [ppid()](#Process.ppid)                         | [num_ctx_switches()](#Process.num_ctx_switches) | [num_threads()](#Process.num_threads)           | [io_counters()](#Process.io_counters)           | [memory_percent()](#Process.memory_percent) | [memory_percent()](#Process.memory_percent) |
| [status()](#Process.status)                     | [num_handles()](#Process.num_handles)           | -                                               | [name()](#Process.name)                         | [num_threads()](#Process.num_threads)       | [num_threads()](#Process.num_threads)       |
| [terminal()](#Process.terminal)                 | [num_threads()](#Process.num_threads)           | [create_time()](#Process.create_time)           | [memory_info()](#Process.memory_info)           | [ppid()](#Process.ppid)                     | [ppid()](#Process.ppid)                     |
| -                                               | [username()](#Process.username)                 | [gids()](#Process.gids)                         | [memory_percent()](#Process.memory_percent)     | [status()](#Process.status)                 | [status()](#Process.status)                 |
| [gids()](#Process.gids)                         | -                                               | [name()](#Process.name)                         | [num_ctx_switches()](#Process.num_ctx_switches) | [terminal()](#Process.terminal)             | [terminal()](#Process.terminal)             |
| [num_ctx_switches()](#Process.num_ctx_switches) | [exe()](#Process.exe)                           | [ppid()](#Process.ppid)                         | [ppid()](#Process.ppid)                         | -                                           | -                                           |
| [num_threads()](#Process.num_threads)           | [name()](#Process.name)                         | [status()](#Process.status)                     | [status()](#Process.status)                     | [gids()](#Process.gids)                     | [gids()](#Process.gids)                     |
| [uids()](#Process.uids)                         | -                                               | [terminal()](#Process.terminal)                 | [terminal()](#Process.terminal)                 | [uids()](#Process.uids)                     | [uids()](#Process.uids)                     |
| [username()](#Process.username)                 | -                                               | [uids()](#Process.uids)                         | [uids()](#Process.uids)                         | [username()](#Process.username)             | [username()](#Process.username)             |
| -                                               | -                                               | [username()](#Process.username)                 | [username()](#Process.username)                 | -                                           | -                                           |
| [memory_full_info()](#Process.memory_full_info) | -                                               | -                                               | -                                               | -                                           | -                                           |
| [memory_maps()](#Process.memory_maps)           | -                                               | -                                               | -                                               | -                                           | -                                           |
| speedup: +2.6x                                  | speedup: +1.8x / +6.5x                          | speedup: +1.9x                                  | speedup: +2.0x                                  | speedup: +1.3x                              | speedup: +1.3x                              |

*5.0.0 版本中新增.*
