# 网络连接信息

**psutil.net_connections(kind='inet')** - [原文](https://psutil.readthedocs.io/en/latest/#psutil.net_connections) <a name="psutil.net_connections"></a>

以命名元组列表的形式返回系统范围的套接字连接。 每个命名元组提供 7 个属性：

- `fd`: 套接字文件描述符。 如果连接指向当前进程，则可以将其传递给 [socket.fromfd][socket.fromfd] 以获得可用的套接字对象。 在 Windows 和 SunOS 上，这始终设置为 `-1`。
- `family`: 地址族，[AF_INET][AF_INET]、[AF_INET6][AF_INET6] 或 [AF_UNIX][AF_UNIX]。
- `type`: 地址类型，[SOCK_STREAM][SOCK_STREAM][SOCK_STREAM]、[SOCK_DGRAM][SOCK_DGRAM] 或 [SOCK_SEQPACKET][SOCK_SEQPACKET]。
- `laddr`: 在 [AF_UNIX][AF_UNIX] 套接字的情况下，本地地址作为`(ip, port)`命名元组或路径(`path`)。 对于 UNIX 套接字，请参阅下面的注释。
- `raddr`: 在 [AF_UNIX][AF_UNIX] 套接字的情况下，远程地址作为`(ip, port)`命名元组或绝对路径(`path`)。当远程端点未连接时，您将获得一个空元组 (AF_INET*) 或 `""` (AF_UNIX)。 对于 UNIX 套接字，请参阅下面的注释。
- `status`: 表示 TCP 连接的状态。 返回值是 [psutil.CONN_*][psutil.CONN_*] 常量之一（字符串）。 对于 UDP 和 UNIX 套接字，这始终是 `psutil.CONN_NONE`。
- `pid`: 如果可检索打开套接字的进程的PID，否则为`None`。 在某些平台（例如 Linux）上，此字段的可用性根据进程权限（需要 root）而变化。

[socket.fromfd]: https://docs.python.org/3/library/socket.html#socket.fromfd "socket.fromfd"
[AF_INET]: https://docs.python.org/zh-cn/3/library/socket.html#socket.AF_INET "AF_INET"
[AF_INET6]: https://docs.python.org/zh-cn/3/library/socket.html#socket.AF_INET6 "AF_INET6"
[AF_UNIX]: https://docs.python.org/zh-cn/3/library/socket.html#socket.AF_UNIX "AF_UNIX"
[SOCK_STREAM]: https://docs.python.org/zh-cn/3/library/socket.html#socket.SOCK_STREAM "SOCK_STREAM"
[SOCK_DGRAM]: https://docs.python.org/zh-cn/3/library/socket.html#socket.SOCK_DGRAM "SOCK_DGRAM"
[SOCK_SEQPACKET]: https://docs.python.org/zh-cn/3/library/socket.html#socket.SOCK_SEQPACKET "SOCK_SEQPACKET"
[psutil.CONN_*]: https://psutil.readthedocs.io/en/latest/#connections-constants "psutil.CONN_* 常量"

**_kind_** 参数是一个字符串，用于过滤符合以下条件的连接：

| Kind 值 | 连接使用                       |
| ------- | ------------------------------ |
| "inet"  | IPv4 和 IPv6                   |
| "inet4" | IPv4                           |
| "inet6" | IPv6                           |
| "tcp"   | TCP                            |
| "tcp4"  | 基于 IPv4 的 TCP               |
| "tcp6"  | 基于 IPv6 的 TCP               |
| "udp"   | UDP                            |
| "udp4"  | 基于 IPv4 的 UDP               |
| "udp6"  | 基于 IPv6 的 UDP               |
| "unix"  | UNIX 套接字（UDP 和 TCP 协议） |
| "all"   | 所有可能的族和协议的总和       |

在 macOS 和 AIX 上，此功能需要 root 权限。 要获得每个进程的连接，请使用 [Process.connections()](#Process.connections)。 另请参阅 [netstat.py][netstat.py] 示例脚本。 例子：

[netstat.py]: https://github.com/giampaolo/psutil/blob/master/scripts/netstat.py "netstat.py"

```python
>>> import psutil
>>> psutil.net_connections()
[pconn(fd=115, family=<AddressFamily.AF_INET: 2>, type=<SocketType.SOCK_STREAM: 1>, laddr=addr(ip='10.0.0.1', port=48776), raddr=addr(ip='93.186.135.91', port=80), status='ESTABLISHED', pid=1254),
 pconn(fd=117, family=<AddressFamily.AF_INET: 2>, type=<SocketType.SOCK_STREAM: 1>, laddr=addr(ip='10.0.0.1', port=43761), raddr=addr(ip='72.14.234.100', port=80), status='CLOSING', pid=2987),
 pconn(fd=-1, family=<AddressFamily.AF_INET: 2>, type=<SocketType.SOCK_STREAM: 1>, laddr=addr(ip='10.0.0.1', port=60759), raddr=addr(ip='72.14.234.104', port=80), status='ESTABLISHED', pid=None),
 pconn(fd=-1, family=<AddressFamily.AF_INET: 2>, type=<SocketType.SOCK_STREAM: 1>, laddr=addr(ip='10.0.0.1', port=51314), raddr=addr(ip='72.14.234.83', port=443), status='SYN_SENT', pid=None)
 ...]
```

**注释**: (macOS 和 AIX) 除非以 root 用户身份运行，否则 [psutil.AccessDenied](#psutil.AccessDenied) 异常总是会抛出。 这是操作系统的限制，`lsof` 也是如此。

**注释**: (Solaris) 不支持 UNIX 套接字。

**注释**: (Linux, FreeBSD) UNIX 套接字的“raddr”字段始终设置为`“”`。 这是操作系统的限制。

**注释**: (OpenBSD) UNIX 套接字的“laddr”和“raddr”字段始终设置为`“”`。 这是操作系统的限制。

*2.1.0 版本中新增.*

*5.3.0 版本中修改: : 套接字“fd”现在设置为实数而不是 `-1`。*

*5.3.0 版本中修改: : “laddr”和“raddr”被命名为元组。*