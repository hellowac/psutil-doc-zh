# 发送信号

**Process.send_signal(signal)** - [原文](https://psutil.readthedocs.io/en/latest/#psutil.Process.send_signal) <a name="Process.send_signal" ></a>

发送信号(参阅 [信号模块手册][信号模块手册])以抢先检查 PID 是否已被重用。在 UNIX 上，这与 `os.kill(pid, sig)` 相同。在 Windows 上仅支持 `SIGTERM` `、CTRL_C_EVENT` 和 `CTRL_BREAK_EVENT` 信号，并且 `SIGTERM` 被视为 [kill()](#Process.kill) 的别名。另请参阅如何[终止进程树](#kill-process-tree)和[终止子进程](#kill-child-process)。

[信号模块手册]: https://docs.python.org//library/signal.html "signal module"

*3.2.0 版本中修改: 添加了对 Windows 上的 `CTRL_C_EVENT` 和 `CTRL_BREAK_EVENT` 信号的支持。*