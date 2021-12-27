# 异常

{{#include ../../links.md}}

## **异常基类**

`class` **psutil.Error** - [原文](https://psutil.readthedocs.io/en/latest/#psutil.Error)

基本异常类。 所有其他异常都继承自这个异常。

## **进程不存在**

`class` **psutil.NoSuchProcess(pid, name=None, msg=None)** - [原文](https://psutil.readthedocs.io/en/latest/#psutil.NoSuchProcess) <a name="psutil.NoSuchProcess"></a>

当在当前进程列表中找不到具有给定 pid 的进程或进程不再存在时，由 [Process] 类的方法抛出。 ***name*** 是进程消失之前的名称，只有在之前调用 [Process.name()] 时才会设置。

## **僵尸进程**

`class` **psutil.ZombieProcess(pid, name=None, ppid=None, msg=None)** - [原文](https://psutil.readthedocs.io/en/latest/#psutil.ZombieProcess) <a name="psutil.ZombieProcess"></a>

在 UNIX 上查询僵尸进程（Windows 没有僵尸进程）时，这可能由 [Process] 类的方法抛出。 如果在进程变成僵尸之前调用 [Process.name()] 或 [Process.ppid()] 方法，则 ***name*** 和 ***ppid*** 属性可用。

**注释**: 这是 [NoSuchProcess](./#进程不存在) 的子类，因此如果对检索僵尸进程不感兴趣（例如，在使用 [process_iter()] 时），可以忽略此异常并只捕获 [NoSuchProcess](./#进程不存在) 。

*3.0.0 版本中新增.*

## **无权限**

`class` **psutil.AccessDenied(pid=None, name=None, msg=None)** - [原文](https://psutil.readthedocs.io/en/latest/#psutil.AccessDenied) <a name="psutil.AccessDenied"></a>

当由于权限不足而拒绝执行操作时，由 [Process] 类的方法抛出。 如果之前调用了 [Process.name()]，则 ***name*** 属性可用。

## **超时**

`class` **psutil.TimeoutExpired(seconds, pid=None, name=None, msg=None)** - [原文](https://psutil.readthedocs.io/en/latest/#psutil.TimeoutExpired) <a name="psutil.TimeoutExpired"></a>

如果超时到期并且进程仍然存在，则由 [Process.wait()] 方法引发。 如果之前调用了 [Process.name()]，则 ***name*** 属性可用。
