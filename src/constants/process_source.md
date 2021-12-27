# 进程资源

{{#include ../links.md}}

参考: [原文](https://psutil.readthedocs.io/en/latest/#process-resources-constants)

- **Linux** / **FreeBSD**:
  - psutil.**RLIM_INFINITY**
  - psutil.**RLIMIT_AS**
  - psutil.**RLIMIT_CORE**
  - psutil.**RLIMIT_CPU**
  - psutil.**RLIMIT_DATA**
  - psutil.**RLIMIT_FSIZE**
  - psutil.**RLIMIT_MEMLOCK**
  - psutil.**RLIMIT_NOFILE**
  - psutil.**RLIMIT_NPROC**
  - psutil.**RLIMIT_RSS**
  - psutil.**RLIMIT_STACK**
- 仅限 **Linux**:
  - psutil.**RLIMIT_LOCKS**
  - psutil.**RLIMIT_MSGQUEUE**
  - psutil.**RLIMIT_NICE**
  - psutil.**RLIMIT_RTPRIO**
  - psutil.**RLIMIT_RTTIME**
  - psutil.**RLIMIT_SIGPENDING**
- 仅限 **FreeBSD**:
  - psutil.**RLIMIT_SWAP**
  - psutil.**RLIMIT_SBSIZE**
  - psutil.**RLIMIT_NPTS**

用于获取和设置与 [psutil.Process.rlimit()][Process.rlimit()] 结合使用的进程资源限制的常量。 有关更多信息，请参阅 [resource.getrlimit]。

*可用平台: Linux, FreeBSD.*

5.7.3 版本中修改: 新增 FreeBSD 支持, 新增 ***RLIMIT_SWAP***, ***RLIMIT_SBSIZE***, ***RLIMIT_NPTS*** 常量.
