# 进程状态

{{#include ../links.md}}

参考: [原文](https://psutil.readthedocs.io/en/latest/#process-status-constants)

- psutil.**STATUS_RUNNING**
- psutil.**STATUS_SLEEPING**
- psutil.**STATUS_DISK_SLEEP**
- psutil.**STATUS_STOPPED**
- psutil.**STATUS_TRACING_STOP**
- psutil.**STATUS_ZOMBIE**
- psutil.**STATUS_DEAD**
- psutil.**STATUS_WAKE_KILL**
- psutil.**STATUS_WAKING**
- psutil.**STATUS_PARKED)**(_Linux_)
- psutil.**STATUS_IDLE)**(_Linux_, _macOS_, _FreeBSD_)
- psutil.**STATUS_LOCKED)**(_FreeBSD_)
- psutil.**STATUS_WAITING)**(_FreeBSD_)
- psutil.**STATUS_SUSPENDED)**(_NetBSD_
  表示进程状态。 由 [psutil.Process.status()][Process.status()] 返回。
  *3.4.1 版本中新增: STATUS_SUSPENDED (NetBSD).*
  *5.4.7 版本中新增: STATUS_PARKED (Linux).*
