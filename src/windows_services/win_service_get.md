# 根据名称获取服务

**psutil.win_service_get(name)** - [原文](https://psutil.readthedocs.io/en/latest/#psutil.win_service_get)<a name="psutil.win_service_get"></a>

按名称获取 Windows 服务，返回 [WindowsService](https://psutil.readthedocs.io/en/latest/#psutil.WindowsService) 实例。 如果不存在具有此类名称的服务，则抛出 [psutil.NoSuchProcess](https://psutil.readthedocs.io/en/latest/#psutil.NoSuchProcess) 异常。

*版本 4.2.0 中新增.*

*可用平台: Windows.*