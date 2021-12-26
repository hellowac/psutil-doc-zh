# 执行目录

**Process.cwd()** - [原文](https://psutil.readthedocs.io/en/latest/#psutil.Process.cwd) <a name="Process.cwd" ></a>

以绝对路径的方式返回进程当前执行目录。

译注例子:

```python
>>> psutil.Process().cwd()
'/xxxx/xxxx/scripts/demo'
```

*5.6.4 版本中修改: 新增 NetBSD 支持。*
