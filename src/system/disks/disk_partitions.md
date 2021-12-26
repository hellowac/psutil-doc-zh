# 挂载信息

**psutil.disk_partitions(all=False)** - [原文](https://psutil.readthedocs.io/en/latest/#psutil.disk_partitions)

将所有挂载的磁盘分区作为命名元组列表返回，包括设备、挂载点和文件系统类型，类似于 UNIX 上的“`df`”命令。如果 **_all_** 参数都为 `False` ，它会尝试仅区分和返回物理设备（例如硬盘、CD-ROM 驱动器、USB 密钥）并忽略所有其他设备（例如伪(pseudo)、内存、重复、无法访问的文件系统）。请注意， **_all_** 参数并非在所有系统上都完全可靠（例如，在 BSD 上，此参数被忽略）。请参阅提供示例用法的 [disk_usage.py][disk_usage.py] 脚本。 返回具有以下字段的命名元组列表：

[disk_usage.py]: https://github.com/giampaolo/psutil/blob/master/scripts/disk_usage.py "disk_usage.py"

- `device`: 设备路径（例如“`/dev/hda1`”）。 在 Windows 上，这是驱动器号（例如“`C:\\`”）。
- `mountpoint`: 挂载点路径（例如“`/`”）。 在 Windows 上，这是驱动器号（例如“`C:\\`”）。
- `fstype`: 分区文件系统（例如 UNIX 上的“`ext3`”或 Windows 上的“`NTFS`”）。
- `opts`: 一个逗号分隔的字符串，指示驱动器/分区的不同挂载选项。 平台相关。
- `maxfile`: 文件名可以具有的最大长度。
- `maxpath`: 路径名（目录名 + 基本文件名）的最大长度。

```python
>>> import psutil
>>> psutil.disk_partitions()
[sdiskpart(device='/dev/sda3', mountpoint='/', fstype='ext4', opts='rw,errors=remount-ro', maxfile=255, maxpath=4096),
 sdiskpart(device='/dev/sda7', mountpoint='/home', fstype='ext4', opts='rw', maxfile=255, maxpath=4096)]
```

_5.7.4 版本中修改: 新增 **maxfile** 和 **maxpath** 字段_