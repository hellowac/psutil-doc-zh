# 温度

**psutil.sensors_temperatures(fahrenheit=False)** - [原文](https://psutil.readthedocs.io/en/latest/#psutil.sensors_temperatures)

返回硬件温度。 每个条目都是一个命名元组，代表某个硬件温度传感器（它可能是 CPU、硬盘或其他东西，取决于操作系统及其配置）。所有温度均以摄氏度表示，除非华氏度(**_fahrenheit_**)设置为 True。 如果操作系统不支持传感器，则返回空字典。 例子：

```python
>>> import psutil
>>> psutil.sensors_temperatures()
{'acpitz': [shwtemp(label='', current=47.0, high=103.0, critical=103.0)],
 'asus': [shwtemp(label='', current=47.0, high=None, critical=None)],
 'coretemp': [shwtemp(label='Physical id 0', current=52.0, high=100.0, critical=100.0),
              shwtemp(label='Core 0', current=45.0, high=100.0, critical=100.0),
              shwtemp(label='Core 1', current=52.0, high=100.0, critical=100.0),
              shwtemp(label='Core 2', current=45.0, high=100.0, critical=100.0),
              shwtemp(label='Core 3', current=47.0, high=100.0, critical=100.0)]}
```

另请参阅示例应用脚本 [temperatures.py][temperatures.py] 和 [sensors.py][sensors.py]。

[temperatures.py]: https://github.com/giampaolo/psutil/blob/master/scripts/temperatures.py "temperatures.py"
[sensors.py]: https://github.com/giampaolo/psutil/blob/master/scripts/sensors.py "sensors.py"

可用平台: Linux, FreeBSD

*5.1.0 版本中新增.*

*5.5.0 版本中修改: 添加了对FreeBSD的支持。*