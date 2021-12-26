# 等待进程终止

**psutil.wait_procs(procs, timeout=None, callback=None)** - [原文](https://psutil.readthedocs.io/en/latest/#psutil.wait_procs)<a name="psutil.wait_proces"></a>

等待 [Process](#psutil.Process) 实例列表终止的快捷函数。 返回一个 `(gone, alive)` 元组，指示哪些进程已经消失，哪些仍然活着。消失的进程实例将有一个新的 ***returncode*** 属性，表示 [Process.wait()](#Process.wait) 返回的进程退出状态。***callback*** 参数是一个函数，当正在等待的进程之一终止并且 [Process](#psutil.Process) 实例作为回调参数传递时会被调用（该实例还将具有 ***returncode*** 属性集合）。一旦所有进程终止或超时（单位:秒）发生，此函数将返回。 与 [Process.wait()](#Process.wait) 不同，如果发生超时，它不会引发 [TimeoutExpired](#psutil.TimeoutExpired)。 一个典型的用例可能是：

- 将 ***SIGTERM*** 信号发送到进程列表
- 给他们一些时间来终止
- 发送 ***SIGKILL*** 给那些还活着的进程

终止并等待此进程的所有子进程的示例：

```python
import psutil

def on_terminate(proc):
    print("process {} terminated with exit code {}".format(proc, proc.returncode))

procs = psutil.Process().children()
for p in procs:
    p.terminate()

gone, alive = psutil.wait_procs(procs, timeout=3, callback=on_terminate)
for p in alive:
    p.kill()
```
