# 父进程列表

**Process.parents()** - [原文](https://psutil.readthedocs.io/en/latest/#psutil.Process.parents) <a name="Process.parents" ></a>

以列表形式返回当前进程的所有父进程的实例方法, 如果没有父进程，返回空列表。同样参考 [ppid()](#Process.ppid) 和 [parent()](#Process.parent) 方法.

译注例子:

```python
>>> psutil.Process().parents()
[psutil.Process(pid=79791, name='zsh', status='running', started='2021-12-09 17:23:11'), psutil.Process(pid=3483, name='Code Helper (Renderer)', status='running', started='2021-12-02 16:07:48'), psutil.Process(pid=3479, name='Code Helper (Renderer)', status='running', started='2021-12-02 16:07:48'), psutil.Process(pid=471, name='Electron', status='running', started='2021-12-02 16:07:35'), psutil.Process(pid=1, name='launchd', status='running', started='2021-12-02 16:07:20'), psutil.Process(pid=0, name='kernel_task', status='running', started='2021-12-02 16:07:20')]
```

*5.6.0 版本中新增.*
