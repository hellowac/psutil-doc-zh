# 内存信息

**Process.memory_info()** - [原文](https://psutil.readthedocs.io/en/latest/#psutil.Process.memory_info) <a name="Process.memory_info" ></a>

返回具有变量字段的命名元组，具体取决于表示有关进程的内存信息的平台。 所有平台上可用的 ***“portable”*** 字段是 `rss` 和 `vms` 。 所有数字都以字节表示。

| Linux  | macOS   | BSD   | Solaris | AIX | Windows                |
| ------ | ------- | ----- | ------- | --- | ---------------------- |
| rss    | rss     | rss   | rss     | rss | rss(`wset`的别名 )     |
| vms    | vms     | vms   | vms     | vms | vms (`pagefile`的别名) |
| shared | pfaults | text  | -       | -   | num_page_faults        |
| text   | pageins | data  | -       | -   | peak_wset              |
| lib    | -       | stack | -       | -   | wset                   |
| data   | -       | -     | -       | -   | peak_paged_pool        |
| dirty  | -       | -     | -       | -   | paged_pool             |
| -      | -       | -     | -       | -   | peak_nonpaged_pool     |
| -      | -       | -     | -       | -   | nonpaged_pool          |
| -      | -       | -     | -       | -   | pagefile               |
| -      | -       | -     | -       | -   | peak_pagefile          |
| -      | -       | -     | -       | -   | private                |

- `rss`: 又名 "**常驻内存大小**"(Resident Set Size), 这是进程使用的非交换物理内存。在 UNIX 上，它匹配“`top`”的 ***RES*** 列）。在 Windows 上，这是 ***wset*** 字段的别名，它匹配 `taskmgr.exe` 的 “Mem Usage” 列。
- `vms`: 又名 “**虚拟内存大小**”(Virtual Memory Size), 这是进程使用的虚拟内存总量。在 UNIX 上，它匹配“`top`”的 ***VIRT*** 列。 在 Windows 上，这是 ***pagefile*** 字段的别名，它匹配 `taskmgr.exe` 的“Mem Usage” “VM Size”列。
- `shared`: (Linux) 可能与其他进程**共享的内存**。 这与`“top”`的 ***SHR*** 列匹配。
- `text` (Linux, BSD): 又名 TRS (text resident set) 专用于可执行代码的内存量。 这与`“top”`的 ***CODE*** 列匹配。
- `data` (Linux, BSD): 又名 DRS (data resident set) 用于非可执行代码的物理内存量。它匹配`“top”`的 ***DATA*** 列。
- `lib` (Linux): 共享库使用的内存。
- `dirty` (Linux): 脏页数。
- `pfaults` (macOS): 页错误数。
- `pageins` (macOS): 实际页面的数量。

对于 Windows 字段的解释依赖于 [PROCESS_MEMORY_COUNTERS_EX][PROCESS_MEMORY_COUNTERS_EX] 结构文档。 Linux 上的示例：

[PROCESS_MEMORY_COUNTERS_EX]: https://docs.microsoft.com/en-us/windows/desktop/api/psapi/ns-psapi-_process_memory_counters_ex "process memory counters ex"

```python
>>> import psutil
>>> p = psutil.Process()
>>> p.memory_info()
pmem(rss=15491072, vms=84025344, shared=5206016, text=2555904, lib=0, data=9891840, dirty=0)
```

*4.0.0 版本中修改: 多个字段返回, 不仅仅是 **rss** 和 **vms**.*

**Process.memory_info_ex()** - [原文](https://psutil.readthedocs.io/en/latest/#psutil.Process.memory_info_ex) <a name="Process.memory_info_ex" ></a>

与 [memory_info()](#Process.memory_info) 相同（已弃用）。

***⚠️警告**:*在 4.0.0 版本中已弃用；使用 [memory_info()](#Process.memory_info) 替换.*