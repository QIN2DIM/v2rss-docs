---
title: "Scaffold Entropy"
weight: 330
# bookFlatSection: false
# bookToc: true
# bookHidden: false
# bookCollapseSection: false
# bookComments: false
# bookSearchExclude: false
---

## Scaffold Entropy

### NAME

main.py entropy - 采集队列的命令行管理工具。

### SYNOPSIS

```bash
main.py entropy <flags>
```

### DESCRIPTION

采集队列的命令行管理工具。功能包括：更新待办任务、更新采集队列容量，检查待办任务心跳，输出采集队列摘要信息。基础用法如下：

```python
Usage: python main.py entropy
______________________________________________________________________
or: python main.py entropy --remote |输出 `远程执行队列` 的摘要信息
or: python main.py entropy --update |将 `本地执行队列` 辐射至远端
or: python main.py entropy --check  |检查 `本地执行队列` 的健康状态
or: python main.py entropy --cap    |将 `POOL_CAP` 队列容量映射到远端
or: python main.py entropy --cap=8  |手动修改远程队列容量
______________________________________________________________________
```

#### Remote Entropy Heap

在 `v6.0.1-alpha `之后，采集器默认使用「远程共享队列」同步待办任务。意味着采集节点不再关心其所在物理服务器中的 `__entropy__` 列表，而是 `Remote EntropyHeap` 对象。

Remote EntropyHeap Object 存储着若干个采集实例的上下文摘要信息，采集器读取这些数据后，根据一系列的生产逻辑，输出符合特征的实例，进而启动采集任务。

手动修改 Remote EntropyHeap 需要执行 ``python main.py entropy --update`` 更新远程共享队列，此时所有采集器节点都会使用新的任务队列。切换操作是立即完成的，在采集器下一次任务预加载时生效。

项目初始化时 Remote EntropyHeap 并不存在，直接执行脚手架 deploy 指令部署采集器后必然会保持空转，也即需要在项目初始化后执行一次 ``python main.py entropy --update`` 用以创建 Remote EntropyHeap，这样采集器才会读取到待办任务。

``--update`` 的逻辑是将本地的 `__entropy__ `辐射到远端，一般在管理员服务器上使用（比如你的本地电脑）。
在后期运维中，管理员发现新的可执行实例时，可以手动编写上下文摘要信息，录入 `__entropy__`，再使用此指令辐射到远程任务队列中。

#### Unified Pool Capacity

在 `v6.0.2-alpha` 之后，可以通过脚手架指令 `entropy --cap` 手动指定远程队列容量，同步操作是立即完成的，将在采集器下次任务预加载时生效。

此指令不会覆盖本地 ``POOL_CAP`` 全局变量的值，也不会覆写任一节点的配置文件，而是创建或更新一个指定的 Redis-Key。

#### Entropy Heartbeat

`--check` 指令可以检查本地队列的健康状态，如摘要信息是否配置正确，`register_url` 的通信状态等。

#### Entropy Status

不携带参数运行可以在控制台输出本地采集队列的摘要信息，添加 `--remote` 参数则输出远程队列的。

### FLAGS

- update=UPDATE
  - Type: bool
  
  - Default: False
  
    将 `本地执行队列` 辐射至远端
  
- remote=REMOTE
  - Type: bool
  
  - Default: False
  
    输出 `远程执行队列` 的摘要信息
  
- check=CHECK
  - Type: bool
  
  - Default: False
  
    检查 `本地执行队列` 的健康状态
  
- cap=CAP
  - Type: Optional[int]
  
  - Default: None
  
    修改远程队列容量

