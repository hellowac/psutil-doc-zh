# 交换内存

**psutil.swap_memory()** - [原文](https://psutil.readthedocs.io/en/latest/#psutil.swap_memory)

将系统交换内存统计信息作为命名元组返回，包括以下字段：

- `total`: 以字节为单位的总交换内存
- `used`: 使用的交换内存（以字节为单位）
- `free`: 以字节为单位的空闲交换内存
- `percent`: 百分比使用率计算为 `(total - available) / total * 100`
- `sin`: 系统从磁盘换入的字节数（累计）
- `sout`: 系统从磁盘换出的字节数（累计）

Windows 上的 **sin** 和 **sout** 始终设置为 0。参阅 [meminfo.py][meminfo.py] 脚本，同时提供了有关如何以可读的形式**转换字节**的示例。

```python
>>> import psutil
>>> psutil.swap_memory()
sswap(total=2097147904L, used=886620160L, free=1210527744L, percent=42.3, sin=1050411008, sout=1906720768)
```

_5.2.3 版本中修改: 在 Linux 上，此函数依赖 /proc fs 而不是 sysinfo() 系统调用，以便它可以与 `psutil.PROCFS_PATH` 结合使用，以检索有关 Linux 容器（例如 Docker 和 Heroku）的内存信息。_