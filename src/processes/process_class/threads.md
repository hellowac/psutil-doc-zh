# 线程

{{#include ../../links.md}}

**Process.threads()** - [原文](https://psutil.readthedocs.io/en/latest/#psutil.Process.threads) <a name="Process.threads" ></a>

将进程打开的线程作为命名元组列表返回。 在 OpenBSD 上，此方法需要 root 权限。

- `id`: 内核分配的原生线程ID。 如果 `pid` 引用当前进程，则与 [threading.Thread] 类的 [native_id][Thread.native_id] 属性匹配，并可将引用用于在当前的 Python 应用程序中运行的各个 Python 线程。
- `user_time`: 在用户模式下花费的时间。
- `system_time`: 在内核模式中花费的时间。
