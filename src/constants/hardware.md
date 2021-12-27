# 硬件

{{#include ../links.md}}

参考: [原文](https://psutil.readthedocs.io/en/latest/#hardware-constants)

- AF_LINK <a name="psutil.AF_LINK"></a>
  标识与网络接口关联的 MAC 地址的常量。 与 [psutil.net_if_addrs()](#psutil.net_if_addrs) 结合使用。
  *3.0.0 版本中新增.*
- NIC_DUPLEX_FULL <a name="psutil.NIC_DUPLEX_FULL"></a>
- NIC_DUPLEX_HALF <a name="psutil.NIC_DUPLEX_HALF"></a>
- NIC_DUPLEX_UNKNOWN <a name="psutil.NIC_DUPLEX_UNKNOWN"></a>
  标识 NIC（网卡）是全速模式还是半速模式的常量。 ***NIC_DUPLEX_FULL*** 表示网卡可以同时发送和接收数据（文件），***NIC_DUPLEX_FULL*** 表示网卡可以一次发送或接收数据。 与 [psutil.net_if_stats()] 结合使用。
  *3.0.0 版本中新增.*
- POWER_TIME_UNKNOWN <a name="psutil.POWER_TIME_UNKNOWN">
- POWER_TIME_UNLIMITED <a name="psutil.POWER_TIME_UNLIMITED">
  电池剩余时间是否无法确定或无限。 可以分配给 [psutil.sensors_battery()] 的 ***secsleft*** 字段。
  5.1.0 版本中新增.
- version_info
  检查 psutil 安装版本的元组。 例子：

  ```python
  >>> import psutil
  >>> if psutil.version_info >= (4, 5):
  ...    pass
  ```
