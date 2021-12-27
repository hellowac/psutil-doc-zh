# 风扇

{{#include ../../links.md}}

**psutil.sensors_fans()** - [原文](https://psutil.readthedocs.io/en/latest/#psutil.sensors_fans)

返回硬件风扇速度。 每个条目都是一个命名元组，代表某个硬件传感器风扇。 风扇速度以 RPM（每分钟转数）表示。 如果操作系统不支持传感器，则返回空字典。 例子：

```python
>>> import psutil
>>> psutil.sensors_fans()
{'asus': [sfan(label='cpu_fan', current=3200)]}
```

另请参阅示例应用脚本 [fans.py] 和 [sensors.py]。

可用平台: Linux

*5.2.0 版本中新增.*
