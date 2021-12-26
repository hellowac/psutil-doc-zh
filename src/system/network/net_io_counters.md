# 网络统计信息

**psutil.net_io_counters(pernic=False, nowrap=True)** - [原文](https://psutil.readthedocs.io/en/latest/#psutil.net_io_counters)

将系统范围的网络 I/O 统计信息作为命名元组返回，包括以下属性：

- `bytes_sent`: 发送的字节数
- `bytes_recv`: 接收的字节数
- `packets_sent`: 发送的数据包数
- `packets_recv`: 收到的数据包数
- `errin`: 接收时的错误总数
- `errout`: 发送时的错误总数
- `dropin`: 丢弃的传入数据包总数
- `dropout`: 丢弃的传出数据包总数（在 macOS 和 BSD 上始终为 0）

如果 **_pernic_** 为 True，则将系统上安装的每个网络接口的相同信息作为字典返回，其中网络接口名称作为键，上面描述的命名元组作为值。在某些系统（例如 Linux）上，在非常繁忙或寿命很长的系统上，内核返回的数字可能会溢出并换行（从零开始）。如果 **_nowrap_** 为 `True` ，psutil 将在函数调用中检测并调整这些数字，并将“旧值”添加到“新值”，以便返回的数字始终增加或保持不变，但永远不会减少。`net_io_counters.cache_clear()` 可用于使 **_nowrap_** 缓存无效。 在没有网络接口的机器上，如果 **_pernic_** 为 `True` ，此函数将返回 `None` 或 `{}`。

```python
>>> import psutil
>>> psutil.net_io_counters()
snetio(bytes_sent=14508483, bytes_recv=62749361, packets_sent=84311, packets_recv=94888, errin=0, errout=0, dropin=0, dropout=0)
>>>
>>> psutil.net_io_counters(pernic=True)
{'lo': snetio(bytes_sent=547971, bytes_recv=547971, packets_sent=5075, packets_recv=5075, errin=0, errout=0, dropin=0, dropout=0),
'wlan0': snetio(bytes_sent=13921765, bytes_recv=62162574, packets_sent=79097, packets_recv=89648, errin=0, errout=0, dropin=0, dropout=0)}
```

示例应用程序另请参阅 [nettop.py][nettop.py] 和 [ifconfig.py][ifconfig.py] 。

[nettop.py]: https://github.com/giampaolo/psutil/blob/master/scripts/nettop.py "nettop.py"
[ifconfig.py]: https://github.com/giampaolo/psutil/blob/master/scripts/ifconfig.py "ifconfig.py"

*5.3.0 版本中修改: 由于新的 **_nowrap_** 参数，数字不再在调用之间换行（从零开始）。*