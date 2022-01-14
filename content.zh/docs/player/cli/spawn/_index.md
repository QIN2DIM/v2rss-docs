---
title: "Scaffold Spawn"
weight: 510
# bookFlatSection: false
# bookToc: true
# bookHidden: false
# bookCollapseSection: false
# bookComments: false
# bookSearchExclude: false
---

## Scaffold Spawn

### NAME

main.py spawn  - 释放所有本机采集实例，基于 gevent 并发执行。

### SYNOPSIS

```bash
main.py spawn <flags>
```

### DESCRIPTION

基础用法如下：

```python
Usage: python main.py nest
______________________________________________________________________
or: python main.py nest --power=4          |指定并发数
or: python main.py nest --remote           |读取远程队列的运行实例
or: python main.py nest --safe             |安全启动，过滤掉需要人机验证的任务
______________________________________________________________________
```

在最佳实践中，仅推荐在调试阶段需要快速补充订阅池的情况下使用，否则请使用 `examples/atomic_go.py` 中的应用案例，通过修改 `alias` 运行指定的采集实例。

这是个对本机硬件配置要求极高的指令，不推荐在少于 `16G` 内存且代理网速不佳的状态下使用。

### FLAGS

- silence=SILENCE
  - Type: bool
  - Default: True
    静默启动
- power=POWER
  - Type: Optional[int]
  - Default: None
    指定并发数
- remote=REMOTE
  - Type: bool
  - Default: False
    将任务队列标记为 ``远程队列``
- safe=SAFE
  - Type: bool
  - Default: False
    安全启动，过滤掉需要人机验证的实例
