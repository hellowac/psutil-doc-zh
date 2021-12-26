# 进程类

`class` **psutil.Process(pid=None)** - [原文](https://psutil.readthedocs.io/en/latest/#psutil.Process) <a name="psutil.Process"></a>

代表具有给定 ***pid*** 的系统(OS)进程。 如果省略 ***pid*** ，则使用当前进程的 ***pid*** ([os.getpid][os.getpid])。 如果 ***pid*** 不存在，则抛出 [NoSuchProcess](#psutil.NoSuchProcess) 异常。 在 Linux 上， ***pid*** 也可以指 线程ID（[threads()](#Process.threads) 方法返回的 ***id*** 字段）。 访问该类的方法时，始终准备捕获 [NoSuchProcess](#psutil.NoSuchProcess) 和 [AccessDenied](#psutil.AccessDenied) 异常。 内建函数 [hash][[builtin.hash]] 可用于此类的实例，以便随着时间的推移唯一地标识进程（hash值由 `进程 PID + 创建时间` 混合后确定）。 因此，它也可以与 [set][typs.set] 一起使用。

**注释**： 为了同时有效地获取有关进程的多个信息，请确保使用 [oneshot()](#Process.oneshot) 上下文管理器或 [as_dict()](#Process.as_dict) 实例方法。

**注释**： 此类和进程绑定的方式是通过其唯一 PID 。这意味着如果进程终止并且操作系统重用其 PID，最终可能会与另一个进程交互。抢先检查进程身份（通过 PID + 创建时间）的唯一例外是以下方法：[nice()](#Process.nice) (set), [ionice()](#Process.ionice) (set), [cpu_affinity()](#Process.cpu_affinity) (set), [rlimit()](#Process.rlimit) (set) , [children()](#Process.children), [parent()](#Process.parent), [parents()](Process.parents), [suspend()](#Process.suspend), [resume()](#Process.resume), [send_signal()](#Process.send_signal), [terminate()](#Process.terminate), [kill()](#Process.kill)。为了防止所有其他方法出现此问题，可以在查询进程之前使用 [is_running()](#Process.is_running) 或 [process_iter()](#psutil.process_iter) 以防迭代所有进程。但必须注意的是，除非处理非常“旧(old)”（非活动(inactive)）的 [Process](#psutil.Process) 实例，否则这几乎不会构成问题。

[os.getpid]: https://docs.python.org/3/library/os.html#os.getpid "os.getpid"
[builtin.hash]: https://docs.python.org/zh-cn/3/library/functions.html#hash "builtin hash"
[typs.set]: https://docs.python.org/zh-cn/3/library/stdtypes.html#types-set. "内置类型 Set"

**译注**: 进程类方法一览

- Process.[oneshot()](#Process.oneshot) - 快照
- Process.[pid](#Process.pid) - 进程ID
- Process.[ppid()](#Process.ppid) - 父进程ID
- Process.[name()](#Process.name) - 进程名称
- Process.[exe()](#Process.exe) - 可执行文件绝对路径
- Process.[cmdline()](#Process.cmdline) - 执行命令行
- Process.[environ()](#Process.environ) - 环境变量
- Process.[create_time()](#Process.create_time) - 创建时间
- Process.[as_dict(attrs=None, ad_value=None)](#Process.as_dict) - 字典信息
- Process.[parent()](#Process.parent) - 父进程
- Process.[parents()](#Process.parents) - 父进程列表
- Process.[status()](#Process.status) - 进程状态
- Process.[cwd()](#Process.cwd) - 执行目录
- Process.[username()](#Process.username) - 所属用户名
- Process.[uids()](#Process.uids) - 用户ID
- Process.[gids()](#Process.gids) - 组ID
- Process.[terminal()](#Process.terminal) - 终端
- Process.[nice(value=None)](#Process.nice) - 优先级
- Process.[ionice(ioclass=None, value=None)](#Process.ionice) - I/O优先级
- Process.[rlimit(resource, limits=None)](#Process.rlimit) - 资源限制
- Process.[io_counters()](#Process.io_counters) - I/O统计
- Process.[num_ctx_switches()](#Process.num_ctx_switches) - 上下文切换数
- Process.[num_fds()](#Process.num_fds) - 文件描述符数
- Process.[num_handles()](#Process.num_handles) - 句柄数
- Process.[num_threads()](#Process.num_threads) - 线程数
- Process.[threads()](#Process.threads) - 线程
- Process.[cpu_times()](#Process.cpu_times) - cpu时间
- Process.[cpu_percent(interval=None)](#Process.cpu_percent) - cpu利用率
- Process.[cpu_affinity(cpus=None)](#Process.cpu_affinity) - cpu亲和度
- Process.[cpu_num()](#Process.cpu_num) - cpu数量
- Process.[memory_info()](#Process.memory_info) - 内存信息
- Process.[memory_info_ex()](#Process.memory_info_ex) - 已废弃
- Process.[memory_full_info()](#Process.memory_full_info) - 内存完全信息
- Process.[memory_percent(memtype="rss")](#Process.memory_percent) - 内存利用率
- Process.[memory_maps(grouped=True)](#Process.memory_maps) - 内存映射
- Process.[children(recursive=False)](#Process.children) - 子进程
- Process.[open_files()](#Process.open_files) - 打开的文件
- Process.[connections(kind="inet")](#Process.connections) - 网络连接
- Process.[is_running()](#Process.is_running) - 是否正在运行
- Process.[send_signal(signal)](#Process.send_signal) - 发送信号
- Process.[suspend()](#Process.suspend) - 暂停进程
- Process.[resume()](#Process.resume) - 恢复进程
- Process.[terminate()](#Process.terminate) - 终止进程
- Process.[kill()](#Process.kill) - 杀死进程
- Process.[wait(timeout=None)](#Process.wait) - 等待
- pstuil.[Popen](#Popen) - 执行子程序
