# cpu亲和度

{{#include ../../links.md}}

**Process.cpu_affinity(cpus=None)** - [原文](https://psutil.readthedocs.io/en/latest/#psutil.Process.cpu_affinity) <a name="Process.cpu_affinity" ></a>

读写当前[CPU亲和度][CPU_affinity]。[CPU亲和度][CPU affinity]包括告诉操作系统仅在一组有限的 CPU 上运行进程（在 Linux 命令行上，通常使用 taskset 命令）。如果没有传递参数，它会以整数列表的形式返回当前的 CPU 亲和性。如果传递参数，它必须是指定新 CPU 关联的整数列表。如果传递空列表，则假定（并设置）所有CPU 都符合条件。在某些系统（例如 Linux）上，所有可用的逻辑CPU并不能用 `list(range(psutil.cpu_count()))` 代表。

```python
>>> import psutil
>>> psutil.cpu_count()
4
>>> p = psutil.Process()
>>> # get
>>> p.cpu_affinity()
[0, 1, 2, 3]
>>> # set; from now on, process will run on CPU #0 and #1 only
>>> p.cpu_affinity([0, 1])
>>> p.cpu_affinity()
[0, 1]
>>> # reset affinity against all eligible CPUs
>>> p.cpu_affinity([])
```

可用平台: Linux, Windows, FreeBSD

*2.2.0 版本中修改: 新增 FreeBSD 支持.*

*5.1.0 版本中修改: 可以传递一个空列表来设置所有 CPU 都符合条件。*
