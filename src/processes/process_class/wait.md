# 等待

{{#include ../../links.md}}

**Process.wait(timeout=None)** - [原文](https://psutil.readthedocs.io/en/latest/#psutil.Process.wait)  <a name="Process.wait" ></a>

等待进程 PID 终止。 有关返回值的详细信息在 UNIX 和 Windows 上有所不同。

在 UNIX: 如果进程正常终止，则返回值是一个正整数 `>= 0` 表示退出代码。 如果进程被信号终止，则返回导致终止的信号的否定值（例如 `-SIGTERM`）。如果 PID 不是 [os.getpid]（当前进程）的子进程，请等待进程消失并返回 `None` 。 如果 PID 不存在，则立即返回 `None` 。

在 Windows: 始终返回退出代码，它是由 [GetExitCodeProcess] 返回的正整数。

***timeout*** 参数以秒表示。 如果指定并且进程仍然活着，则引发 [TimeoutExpired] 异常。 `timeout=0` 可用于非阻塞应用程序：它会立即返回或引发 [TimeoutExpired] 异常。

返回值被缓存。 要等待多个进程，请使用 [psutil.wait_procs()]。

```python
>>> import psutil
>>> p = psutil.Process(9891)
>>> p.terminate()
>>> p.wait()
<Negsignal.SIGTERM: -15>
```

5.7.1 版本中修改: 返回值被缓存（而不是返回 `None` ）。

5.7.1 版本中修改: 在 POSIX 上，如果出现负信号，则将以可读的枚举返回。
