# 网卡状态

**psutil.net_if_stats()** - [原文](https://psutil.readthedocs.io/en/latest/#psutil.net_if_stats) <a name="psutil.net_if_stats"></a>

以字典形式返回系统上安装的每个 NIC（网络接口卡）的信息，其键是 NIC 名称，值是具有以下字段的命名元组：

- `isup`: 一个布尔值，指示 NIC 是否已启用并正在运行（意味着以太网电缆或 Wi-Fi 已连接）。
- `duplex`: 双工通信类型； 它可以是 [NIC_DUPLEX_FULL][NIC_DUPLEX_FULL]、[NIC_DUPLEX_HALF][NIC_DUPLEX_HALF] 或 [NIC_DUPLEX_UNKNOWN][NIC_DUPLEX_UNKNOWN]。
- `speed`: 以兆位 (MB) 表示的 NIC 速度，如果无法确定（例如“本地主机”），它将设置为 `0`。
- `mtu`: NIC 的最大传输单位，以字节为单位。

[NIC_DUPLEX_FULL]: #psutil.NIC_DUPLEX_FULL "psutil.NIC_DUPLEX_FULL"
[NIC_DUPLEX_HALF]: #psutil.NIC_DUPLEX_HALF "psutil.NIC_DUPLEX_HALF"
[NIC_DUPLEX_UNKNOWN]: #psutil.NIC_DUPLEX_UNKNOWN "psutil.NIC_DUPLEX_UNKNOWN"

样例:

```python
>>> import psutil
>>> psutil.net_if_stats()
{'eth0': snicstats(isup=True, duplex=<NicDuplex.NIC_DUPLEX_FULL: 2>, speed=100, mtu=1500),
 'lo': snicstats(isup=True, duplex=<NicDuplex.NIC_DUPLEX_UNKNOWN: 0>, speed=0, mtu=65536)}
```

另请参阅示例应用程序 [nettop.py][nettop.py] 和 [ifconfig.py][ifconfig.py]。

*3.0.0 版本中新增.*

*5.7.3 版本中修改: UNIX 上的 **isup** 同时还会检查 NIC 是否正在运行。*