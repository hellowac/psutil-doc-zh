# cpu数量

**Process.cpu_num()** - [原文](https://psutil.readthedocs.io/en/latest/#psutil.Process.cpu_num) <a name="Process.cpu_num" ></a>

返回此进程当前正在运行的 CPU数。返回值应该 `<=` [psutil.cpu_count()][#psutil.cpu_count]。在 FreeBSD 上，某些内核进程可能返回 `-1`。它可以与 [psutil.cpu_percent(percpu=True)](#psutil.cpu_percent) 结合使用来观察分布在多个 CPU 上的系统工作负载，如 [cpu_distribution.py][cpu_distribution.py] 示例脚本所示。

[cpu_distribution.py]: https://github.com/giampaolo/psutil/blob/master/scripts/cpu_distribution.py "cpu_distribution.py"

*可用平台: Linux, FreeBSD, SunOS。*

5.1.0 版本中新增.