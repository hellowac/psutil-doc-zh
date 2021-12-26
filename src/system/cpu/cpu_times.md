# 执行时间

**psutil.cpu_times(percpu=False)** - [原文](https://psutil.readthedocs.io/en/latest/#psutil.cpu_times) <a name="psutil.cpu_times"></a>

返回一个命名元组的CPU时间信息，每个属性代表 CPU 在给定模式下花费的秒数。 属性可用性因平台而异。

- **user**: 进程在用户模式(user mode)下执行所花费的时间； 在 Linux 上，这也包括访客时间(guest time)。
- **system**: 进程在内核模式(kernel mode)下执行所花费的时间。
- **idle**: 空闲时间。

特定平台的字段:

- **nice** (UNIX): niced(优先) 进程在用户模式(user mode)下所花费的时间; 在 Linux 上，这也包括访客优先时间(guest_nice time)。
- **iowait** (Linux): 等待 I/O 完成所花费的时间。 这不计入空闲时间中。
- **irq** (Linux, BSD): 服务硬件中断所花费的时间。
- **softirq** (Linux): 服务软件中断所花费的时间。
- **steal** (Linux 2.6.11+): 在虚拟化环境中运行的其他操作系统所花费的时间。
- **guest** (Linux 2.6.24+): 在 Linux 内核的控制下为客户操作系统运行虚拟 CPU 所花费的时间
- **guest_nice** (Linux 3.2.0+): niced(优先) 访客进程所花费的时间 (用于在 Linux 内核控制下的客户操作系统的虚拟 CPU)
- **interrupt** (Windows): 服务硬件中断所花费的时间 ( 类似于 UNIX 上的“irq”)
- **dpc** (Windows): 服务延迟过程调用服务中断 (DPC) 所花费的时间； DPC 是运行优先级低于标准中断(interrupts)的中断。

**译注**: DPC是“Deferred Procedure Call”的缩写，意为推迟了的过程（函数）调用。参考: [延迟过程调用][windows-dpc]

当 _percpu_ 为 `True` 时，返回系统上每个逻辑 CPU 的命名元组列表。 列表的第一个元素指的是第一个 CPU，第二个元素指的是第二个 CPU，依此类推。 列表的顺序在调用之间是一致的。 Linux 上的示例输出：

```python
>>> import psutil
>>> psutil.cpu_times()
scputimes(user=17411.7, nice=77.99, system=3797.02, idle=51266.57, iowait=732.58, irq=0.01, softirq=142.43, steal=0.0, guest=0.0, guest_nice=0.0)
```

4.1.0 版本中更新: 对于Windows平台新增 **_interrupt_** 和 **_dpc_** 字段.

**⚠️警告**: CPU 时间总是应该随着时间的推移而增加，或者至少保持不变，那是因为时间不能倒流。令人惊讶的是，有时情况并非如此（至少在 Windows 和 Linux 上）, 参考 [#1210][issue-1210].

[issue-1210]: https://github.com/giampaolo/psutil/issues/1210#issuecomment-363046156 "CPU steal stuck at 100%"
[windows-dpc]: https://zh.wikipedia.org/wiki/%E5%BB%B6%E8%BF%9F%E8%BF%87%E7%A8%8B%E8%B0%83%E7%94%A8 "延迟过程调用"
