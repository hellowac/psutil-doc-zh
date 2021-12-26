# 网络连接

**Process.connections(kind="inet")** - [原文](https://psutil.readthedocs.io/en/latest/#psutil.Process.connections) <a name="Process.connections" ></a>

将进程打开的socket连接作为命名元组列表返回。要获得系统范围的连接，请使用 [psutil.net_connections()](#psutil.net_connections)。 每个命名元组提供 6 个属性：

- `fd`: 套接字文件描述符。 这可以传递给 [socket.fromfd][socket.fromfd] 以获得可用的套接字对象。在 Windows、FreeBSD 和 SunOS 上，它始终设置为 -1。
- `family`: 地址族，[AF_INET][AF_INET]、[AF_INET6][AF_INET6] 或 [AF_UNIX][AF_UNIX] 。
- `type`: 地址类型，[SOCK_STREAM][SOCK_STREAM] 、[SOCK_DGRAM][SOCK_DGRAM] 或 [SOCK_SEQPACKET][SOCK_SEQPACKET] 。
- `laddr`: 在 [AF_UNIX][AF_UNIX] 套接字的情况下，本地地址作为 `(ip, port)` 命名元组或路径。 对于 UNIX 套接字，请参阅下面的注释。
- `raddr`: 在 UNIX 套接字的情况下，远程地址作为`(ip, port)` 命名元组或绝对路径。 当远程端点未连接时，您将获得一个空元组 (**AF_INET\***) 或 `""` (**AF_UNIX**)。 对于 UNIX 套接字，请参阅下面的注释。
- `status`: 表示 TCP 连接的状态。 返回值是 [psutil.CONN_*](#connections-constants) 常量之一。 对于 UDP 和 UNIX 套接字，这始终是 [psutil.CONN_NONE](#psutil.CONN_NONE)。

[socket.fromfd]: https://docs.python.org/zh-cn/3/library/socket.html#socket.fromfd "socket.fromfd"

***kind*** 参数是一个字符串，用于过滤符合以下条件的连接：

| Kind 值   | 网络连接使用                   |
| --------- | ------------------------------ |
| `"inet"`  | IPv4 和 IPv6                   |
| `"inet4"` | IPv4                           |
| `"inet6"` | IPv6                           |
| `"tcp"`   | TCP                            |
| `"tcp4"`  | 基于 IPv4 的 TCP               |
| `"tcp6"`  | 基于 IPv6 的 TCP               |
| `"udp"`   | UDP                            |
| `"udp4"`  | 基于 IPv4 的 UDP               |
| `"udp6"`  | 基于 IPv6 的 UDP               |
| `"unix"`  | UNIX 套接字（UDP 和 TCP 协议） |
| `"all"`   | 所有可能的族和协议的总和       |

例子:

```python
>>> import psutil
>>> p = psutil.Process(1694)
>>> p.name()
'firefox'
>>> p.connections()
[pconn(fd=115, family=<AddressFamily.AF_INET: 2>, type=<SocketType.SOCK_STREAM: 1>, laddr=addr(ip='10.0.0.1', port=48776), raddr=addr(ip='93.186.135.91', port=80), status='ESTABLISHED'),
pconn(fd=117, family=<AddressFamily.AF_INET: 2>, type=<SocketType.SOCK_STREAM: 1>, laddr=addr(ip='10.0.0.1', port=43761), raddr=addr(ip='72.14.234.100', port=80), status='CLOSING'),
pconn(fd=119, family=<AddressFamily.AF_INET: 2>, type=<SocketType.SOCK_STREAM: 1>, laddr=addr(ip='10.0.0.1', port=60759), raddr=addr(ip='72.14.234.104', port=80), status='ESTABLISHED'),
pconn(fd=123, family=<AddressFamily.AF_INET: 2>, type=<SocketType.SOCK_STREAM: 1>, laddr=addr(ip='10.0.0.1', port=51314), raddr=addr(ip='72.14.234.83', port=443), status='SYN_SENT')]
```

**注释**: *(Solaris) 不支持 UNIX 套接字。*

**注释**: *(Linux, FreeBSD) UNIX 套接字的“**raddr**”字段始终设置为`“”`。 这是操作系统的限制。*

**注释**: (OpenBSD) *UNIX 套接字的“**laddr**”和“**raddr**”字段始终设置为`“”`。 这是操作系统的限制。*

**注释**: (AIX) [psutil.AccessDenied](#psutil.AccessDenied) 异常总是抛出，除非以 `root` 身份运行（`lsof` 也是如此）。

*5.3.0 版本中修改: : “**laddr**”和“**raddr**”被命名为元组。*