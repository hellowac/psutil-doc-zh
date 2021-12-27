# 进程名称

{{#include ../../links.md}}

**Process.name()** - [原文](https://psutil.readthedocs.io/en/latest/#psutil.Process.name) <a name="Process.name" ></a>

返回进程名称. 在 Windows 上，第一次调用后会缓存返回值。在 POSIX 类型机器上时则不会缓存， 因为进程名称可能会改变。 另请参阅如何[按名称查找进程]。
