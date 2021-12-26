# win服务类

`class` **psutil.WindowsService** - [原文](https://psutil.readthedocs.io/en/latest/#psutil.WindowsService)

表示具有给定名称的 Windows 服务。 此类由 [win_service_iter()](#psutil.win_service_iter) 和 [win_service_get()](#psutil.win_service_get) 函数返回，不应直接实例化。

- `name`() - [原文](https://psutil.readthedocs.io/en/latest/#psutil.WindowsService.name)
    服务名称. 此字符串是引用服务的方式，可以传递给 [win_service_get()](#psutil.win_service_get) 获取一个新的 WindowsService 实例。
- `display_name`() - [原文](https://psutil.readthedocs.io/en/latest/#psutil.WindowsService.display_name)
    服务显示名称。当这个类被实例化时，该值被缓存。
- `binpath`() - [原文](https://psutil.readthedocs.io/en/latest/#psutil.WindowsService.binpath)
    作为字符串的服务二进制/exe 文件的完全限定路径，包括命令行参数。
- `username`() - [原文](https://psutil.readthedocs.io/en/latest/#psutil.WindowsService.username)
    拥有此服务的用户的名称。
- `start_type`() - [原文](https://psutil.readthedocs.io/en/latest/#psutil.WindowsService.start_type)
    一个字符串，可以是“自动”(automatic)、“手动”(manual)或“禁用”(disabled)。
- `pid`() - [原文](https://psutil.readthedocs.io/en/latest/#psutil.WindowsService.pid)
    进程 PID，如果有，否则为 `None` 。 这可以传递给 [Process](#psutil.Process) 类来控制服务的进程。
- `status`() - [原文](https://psutil.readthedocs.io/en/latest/#psutil.WindowsService.status)
    服务状态为字符串，可以是“running”、“paused”、“start_pending”、“pause_pending”、“continue_pending”、“stop_pending”或“stopped”。
- `description`() - [原文](https://psutil.readthedocs.io/en/latest/#psutil.WindowsService.description)
    服务详细说明。
- `as_dict`()- [原文](https://psutil.readthedocs.io/en/latest/#psutil.WindowsService.as_dict)
    将上述所有信息作为字典检索的实例方法。

*版本 4.2.0 中新增.*

*可用平台: Windows.*

演示代码:

```python
>>> import psutil
>>> list(psutil.win_service_iter())
[<WindowsService(name='AeLookupSvc', display_name='Application Experience') at 38850096>,
<WindowsService(name='ALG', display_name='Application Layer Gateway Service') at 38850128>,
<WindowsService(name='APNMCP', display_name='Ask Update Service') at 38850160>,
<WindowsService(name='AppIDSvc', display_name='Application Identity') at 38850192>,
...]
>>> s = psutil.win_service_get('alg')
>>> s.as_dict()
{'binpath': 'C:\\Windows\\System32\\alg.exe',
'description': 'Provides support for 3rd party protocol plug-ins for Internet Connection Sharing',
'display_name': 'Application Layer Gateway Service',
'name': 'alg',
'pid': None,
'start_type': 'manual',
'status': 'stopped',
'username': 'NT AUTHORITY\\LocalService'}
```
