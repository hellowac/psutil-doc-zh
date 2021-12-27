# 打开的文件

{{#include ../../links.md}}

**Process.open_files()** - [原文](https://psutil.readthedocs.io/en/latest/#psutil.Process.open_files) <a name="Process.open_files" ></a>

以命名元组列表返回进程打开的常规文件，包括以下字段：

- `path`: 绝对文件名。
- `fd`: 文件描述符编号； 在 Windows 上，这始终是 -1。

仅限 Linux：

- `position` (Linux): 文件（偏移）位置。
- `mode` (Linux): 一个字符串，指示文件是如何打开的，类似于 [open][builtin-open] 内置模式参数。 可能的值为`“r”`、`“w”`、`“a”`、`“r+”`和`“a+”`。 以二进制或文本模式（`“b”`或`“t”`）打开的文件之间没有区别。
- `flags` (Linux): 打开文件时传递给底层 C 调用 [os.open][os-open] 的标志（例如 [os.O_RDONLY]、[os.O_TRUNC] 等）。

```python
>>> import psutil
>>> f = open('file.ext', 'w')
>>> p = psutil.Process()
>>> p.open_files()
[popenfile(path='/home/giampaolo/svn/psutil/file.ext', fd=3, position=0, mode='w', flags=32769)]
```

**⚠️警告**: 在 Windows 上，由于底层 Windows API 的一些限制，在检索某些文件句柄时可能会挂起，因此此方法不可靠。 为了解决这个问题，psutil 会生成一个线程来确定文件句柄名称，如果它在 100 毫秒后没有响应，则将其杀死。这意味着 Windows 上的此方法不能保证枚举所有常规文件句柄（请参阅[问题 597][issue-597]）。 像 ***ProcessHacker*** 这样的工具也有同样的限制。

**⚠️警告**: 在 BSD 上，由于内核错误，此方法可以返回带有空路径（`“”`）的文件，因此它不可靠（请参阅[问题 597][issue-597]）。

*3.1.0 版本中修改: 不再挂在 Windows 上。*

*4.1.0 版本中修改: Linux平台中新增 **position** , **mode** 和 **flags** 字段。*
