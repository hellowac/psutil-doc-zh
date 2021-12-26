# 网络连接信息

**psutil.net_if_addrs()** - [原文](https://psutil.readthedocs.io/en/latest/#psutil.net_if_addrs) <a name="psutil.net_if_addrs"></a>

返回与系统上安装的每个 NIC（网络接口卡）关联的地址作为字典，其键是 NIC 名称，值是分配给 NIC 的每个地址的命名元组列表。 每个命名元组包括 5 个字段：

- `family`: 地址族，[AF_INET][AF_INET] 或 [AF_INET6][AF_INET6] 或 [psutil.AF_LINK](#psutil.AF_LINK)，指的是 MAC 地址。
- `address`: 主 NIC 地址（始终设置）。
- `netmask`: 网络掩码地址（可能是 `None` ）。
- `broadcast`: 广播地址（可能是 `None` ）。
- `ptp`: 代表“点对点”(point to point)； 它是点对点接口（通常是 VPN）上的目标地址。 广播和 ptp 是互斥的。 可能为 `None`。

样例:

```python
>>> import psutil
>>> psutil.net_if_addrs()
{'lo': [snicaddr(family=<AddressFamily.AF_INET: 2>, address='127.0.0.1', netmask='255.0.0.0', broadcast='127.0.0.1', ptp=None),
        snicaddr(family=<AddressFamily.AF_INET6: 10>, address='::1', netmask='ffff:ffff:ffff:ffff:ffff:ffff:ffff:ffff', broadcast=None, ptp=None),
        snicaddr(family=<AddressFamily.AF_LINK: 17>, address='00:00:00:00:00:00', netmask=None, broadcast='00:00:00:00:00:00', ptp=None)],
 'wlan0': [snicaddr(family=<AddressFamily.AF_INET: 2>, address='192.168.1.3', netmask='255.255.255.0', broadcast='192.168.1.255', ptp=None),
           snicaddr(family=<AddressFamily.AF_INET6: 10>, address='fe80::c685:8ff:fe45:641%wlan0', netmask='ffff:ffff:ffff:ffff::', broadcast=None, ptp=None),
           snicaddr(family=<AddressFamily.AF_LINK: 17>, address='c4:85:08:45:06:41', netmask=None, broadcast='ff:ff:ff:ff:ff:ff', ptp=None)]}
>>>
```

另请参阅示例应用程序 [nettop.py][nettop.py] 和 [ifconfig.py][ifconfig.py]。

**注释**: 如果对其他协议家族（例如 AF_BLUETOOTH）感兴趣，可以使用更强大的 [netifaces][netifaces] 扩展。

**Note**: 你可以有多个相同系列的地址与每个接口相关联（这就是为什么 dict 值是列表）。

**Note**: Windows 不支持广播和 ptp，并且始终为 `None` 。

[netifaces]: https://pypi.org/project/netifaces/ "netifaces"

*3.0.0 版本中新增.*

*3.2.0 版本中修改: 添加了 **ptp** 字段。*

*4.4.0 版本中修改: 添加了对 Windows 上不再是 `None` 的网络掩码字段的支持。*