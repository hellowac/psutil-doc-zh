# 网络连接

参考: [原文](https://psutil.readthedocs.io/en/latest/#connections-constants)

- psutil.**CONN_ESTABLISHED**
- psutil.**CONN_SYN_SENT**
- psutil.**CONN_SYN_RECV**
- psutil.**CONN_FIN_WAIT1**
- psutil.**CONN_FIN_WAIT2**
- psutil.**CONN_TIME_WAIT**
- psutil.**CONN_CLOSE**
- psutil.**CONN_CLOSE_WAIT**
- psutil.**CONN_LAST_ACK**
- psutil.**CONN_LISTEN**
- psutil.**CONN_CLOSING**
- psutil.**CONN_NONE**  <a name="psutil.CONN_NONE"></a>
- psutil.**CONN_DELETE_TCB**(_Windows_)
- psutil.**CONN_IDLE**(_Solaris_)
- psutil.**CONN_BOUND**(_Solaris_)

一组表示 TCP 连接状态的字符串。 由 [psutil.Process.connections()](#Process.connections) 和 [psutil.net_connections()](#psutil.net_connections)（status 字段）返回。