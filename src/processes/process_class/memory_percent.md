# 内存利用率

{{#include ../../links.md}}

**Process.memory_percent(memtype="rss")** - [原文](https://psutil.readthedocs.io/en/latest/#psutil.Process.memory_percent) <a name="Process.memory_percent" ></a>

将进程内存与总物理系统内存进行比较，并以百分比形式计算进程内存利用率。 ***memtype*** 参数是一个字符串，它指示您要比较的进程内存类型。您可以在 [memory_info()] 和 [memory_full_info()] 返回的命名元组字段名称之间进行选择（默认为“***rss***”）。

*4.0.0 版本中修改: 新增 **memtype** 参数.*
