# 统计信息

**psutil.cpu_stats()** - [原文](https://psutil.readthedocs.io/en/latest/#psutil.cpu_stats)

将各种 CPU 统计信息作为命名元组返回:

- **ctx_switches**: 自启动以来的上下文切换次数（自愿 + 非自愿）.
- **interrupts**: 自启动以来的中断数.
- **soft_interrupts**: 自启动以来的软件中断数。 在 Windows 和 SunOS 上始终设置为 0.
- **syscalls**: 自启动以来的系统调用数。 在 Linux 上始终设置为 0.

样例 (Linux):

```python
>>> import psutil
>>> psutil.cpu_stats()
scpustats(ctx_switches=20455687, interrupts=6598984, soft_interrupts=2134212, syscalls=0)
```

_4.1.0 版本中新增。_
