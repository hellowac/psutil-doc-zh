# 进程优先级

{{#include ../links.md}}

参考: [原文](https://psutil.readthedocs.io/en/latest/#process-priority-constants)

- psutil.**REALTIME_PRIORITY_CLASS**
- psutil.**HIGH_PRIORITY_CLASS**
- psutil.**ABOVE_NORMAL_PRIORITY_CLASS**
- psutil.**ABOVE_NORMAL_PRIORITY_CLASS**
- psutil.**NORMAL_PRIORITY_CLASS**
- psutil.**IDLE_PRIORITY_CLASS**
- psutil.**BELOW_NORMAL_PRIORITY_CLASS**
  表示 Windows 上进程的优先级（请参阅 [SetPriorityClass]）。 它们可以与 [psutil.Process.nice()][Process.nice()] 结合使用来获取或设置进程优先级。
  可用平台: Windows
- psutil.**IOPRIO_CLASS_NONE**
- psutil.**IOPRIO_CLASS_RT**
- psutil.**IOPRIO_CLASS_BE**
- psutil.**IOPRIO_CLASS_IDLE**
  一组整数，表示 Linux 上进程的 I/O 优先级。 它们可以与 [psutil.Process.nice()][Process.nice()] 结合使用来获取或设置进程 I/O 优先级。 ***IOPRIO_CLASS_NONE*** 和 ***IOPRIO_CLASS_BE*** （尽力而为）是任何未设置特定 I/O 优先级的进程的默认值。***IOPRIO_CLASS_RT***（实时）意味着进程将首先访问磁盘，而不管系统中发生了什么。 ***IOPRIO_CLASS_IDLE*** 意味着当没有其他人需要磁盘时，进程将获得 I/O 时间。 有关更多信息，请参阅 [ionice][ionice] 命令行实用程序或 [ioprio_get] 系统调用的手册。
  可用平台: Linux
- psutil.**IOPRIO_VERYLOW**
- psutil.**IOPRIO_LOW**
- psutil.**IOPRIO_NORMAL**
- psutil.**IOPRIO_HIGH**
  一组整数，表示 Windows 上进程的 I/O 优先级。 它们可以与 [psutil.Process.nice()][Process.nice()] 结合使用来获取或设置进程 I/O 优先级。
  *可用平台: Windows.*
  *5.6.2 版本中新增.*
