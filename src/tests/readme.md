# 测试

参考: [原文](https://psutil.readthedocs.io/en/latest/#running-tests)

```python
python3 -m psutil.tests
```

## debug模式 (Debug mode) - [原文](https://psutil.readthedocs.io/en/latest/#debug-mode)

如果想调试异常情况或报告一个漏洞，使用环境变量`PSUTIL_DEBUG`开启调试模式将会非常有用。在调试模式中，psutil会(或者不会)打印额外的信息到标准错误输出(stderr)。通常这些错误情况并不严重，因此常被忽略（防止崩溃）。在调试模式启动时单元测试是自动运行的。在Unix中：

```python
$ PSUTIL_DEBUG=1 python3 script.py
psutil-debug [psutil/_psutil_linux.c:150]> setmntent() failed (ignored)
```

在windows系统中:

```python
set PSUTIL_DEBUG=1 python.exe script.py
psutil-debug [psutil/arch/windows/process_info.c:90]> NtWow64ReadVirtualMemory64(pbi64.PebBaseAddress) -> 998 (Unknown error) (ignored)
```
