# 常见问题

参考: [原文](https://psutil.readthedocs.io/en/latest/#faqs)

- Q: 为什么某些进程我会无权限?
- A: 当你查询其他用户拥有的进程时可能会发生这种情况，尤其是在 macOS (参考[问题 #883](https://github.com/giampaolo/psutil/issues/883)) 和 Windows 上。不幸的是，除了以更高的权限运行 Python 进程之外，对此无能为力。 在 Unix 上，你可以以 root 身份运行 Python 进程或使用 SUID 位（ps 和 netstat 执行此操作）。 在 Windows 上，你可以将 Python 进程作为 NT AUTHORITY\SYSTEM 运行，或者将 Python 脚本安装为 Windows 服务（ProcessHacker 执行此操作）。
- Q: 支持在windows系统的MinGW上运行吗?
- A: 不支持, 你应该使用 Visual Studio (参阅 [开发指南](https://github.com/giampaolo/psutil/blob/master/docs/DEVGUIDE.rst)).
