# 操作系统

参考: [原文](https://psutil.readthedocs.io/en/latest/#operating-system-constants)

- psutil.**POSIX**
- psutil.**LINUX**
- psutil.**WINDOWS**
- psutil.**MACOS**
- psutil.**FREEBSD**
- psutil.**NETBSD**
- psutil.**OPENBSD**
- psutil.**BSD**
- psutil.**SUNOS**
- psutil.**AIX**
  `bool` 常量, 该常量定义了你属于什么平台. 例如: 如果在Windows平台, **WINDOWS** 常量将会为 `True`, 其他平台将会为 `False`.
  版本 4.0.0. 中新增
  版本 5.4.0 中改变过: 新增 AIX

- psutil.**OSX**
  **MACOS** 的别名.
  **注意**: 版本 5.4.7 中已弃用; 使用 **MACOS** 替换.
  
- psutil.**PROCFS_PATH**
  Linux、Solaris 和 AIX 上 /proc 文件系统的路径（默认为`“/proc”`）。您可能希望在导入 psutil 后立即重新设置此常量，以防您的 /proc 文件系统安装在其他地方，或者您想检索有关 Linux 容器（如 Docker、Heroku 或 LXC）的信息（请参阅[此处](https://fabiokung.com/2014/03/13/memory-inside-linux-containers/)了解更多信息）。必须注意的是，此技巧仅适用于依赖 /proc 文件系统的 API（例如[内存 API](#内存-Memory)和大多数 [Process](#psutil.Process) 类方法）。
  可用平台: Linux, Solaris, AIX
  *3.2.3 版本中新增.*
  *3.4.2 版本中修改: 也可在 Solaris 上使用。*
  *5.4.0 版本中修改: 也可以在 AIX 上使用。*
