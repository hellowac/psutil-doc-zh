# 内存映射

{{#include ../../links.md}}

**Process.memory_maps(grouped=True)** - [原文](https://psutil.readthedocs.io/en/latest/#psutil.Process.memory_maps) <a name="Process.memory_maps" ></a>

将进程的映射内存区域作为命名元组列表返回，其字段根据平台而变化。 此方法可用于获取进程内存使用情况的详细表示，如此处所述（最重要的值是“**私有**(private)”内存）。如果 ***grouped*** 为 `True`，则具有相同路径的映射区域将组合在一起，并且将不同的内存字段相加。如果 ***grouped*** 为 `False` ，则每个映射区域都显示为单个实体，命名元组还将包括映射区域的地址空间 (***addr***) 和权限集 (***perms***)。 有关示例应用程序，请参阅 [pmap.py]。

| Linux         | Windows | FreeBSD      | Solaris   |
| ------------- | ------- | ------------ | --------- |
| rss           | rss     | rss          | rss       |
| size          | -       | private      | anonymous |
| pss           | -       | ref_count    | locked    |
| shared_clean  | -       | shadow_count | -         |
| shared_dirty  | -       | -            | -         |
| private_clean | -       | -            | -         |
| private_dirty | -       | -            | -         |
| referenced    | -       | -            | -         |
| anonymous     | -       | -            | -         |
| swap          | -       | -            | -         |

```python
>>> import psutil
>>> p = psutil.Process()
>>> p.memory_maps()
[pmmap_grouped(path='/lib/x8664-linux-gnu/libutil-2.15.so', rss=32768, size=2125824, pss=32768, shared_clean=0, shared_dirty=0, private_clean=20480, private_dirty=12288, referenced=32768, anonymous=12288, swap=0),
pmmap_grouped(path='/lib/x8664-linux-gnu/libc-2.15.so', rss=3821568, size=3842048, pss=3821568, shared_clean=0, shared_dirty=0, private_clean=0, private_dirty=3821568, referenced=3575808, anonymous=3821568, swap=0),
...]
```

*可用平台: Linux, Windows, FreeBSD, SunOS。*

5.6.0 版本中修改: 删除 macOS 支持，因为天生就坏了(参见[问题#1291][issue-1291])
