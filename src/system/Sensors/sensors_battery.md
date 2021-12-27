# 电池

{{#include ../../links.md}}

**psutil.sensors_battery()** - [原文](https://psutil.readthedocs.io/en/latest/#psutil.sensors_battery) <a name="psutil.sensors_battery"></a>

将电池状态信息作为包含以下值的命名元组返回。 如果未安装电池或无法确定指标，则返回 `None` 。

- `percent`: 电池电量剩余百分比。
- `secsleft`: 电池电量耗尽前还剩多少秒的粗略近似值。 如果连接了交流电源线，则此项设置为 [psutil.POWER_TIME_UNLIMITED]。 如果无法确定，则将其设置为 [psutil.POWER_TIME_UNKNOWN]。
- `power_plugged`: 如果 AC 电源线已连接，则为 `True` ，否则为 `False` ，如果无法确定则为 `None` 。

例子:

```python
>>> import psutil
>>>
>>> def secs2hours(secs):
...     mm, ss = divmod(secs, 60)
...     hh, mm = divmod(mm, 60)
...     return "%d:%02d:%02d" % (hh, mm, ss)
...
>>> battery = psutil.sensors_battery()
>>> battery
sbattery(percent=93, secsleft=16628, power_plugged=False)
>>> print("charge = %s%%, time left = %s" % (battery.percent, secs2hours(battery.secsleft)))
charge = 93%, time left = 4:37:08
```

另请参阅示例应用脚本 [battery.py] 和 [sensors.py]。

可用平台: Linux, Windows, FreeBSD

*5.1.0 版本中新增.*

*5.4.2 版本中修改: 添加了 macOS 支持.*
