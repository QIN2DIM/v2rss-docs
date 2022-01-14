---
title: "Scaffold Deploy"
weight: 300
# bookFlatSection: false
# bookToc: true
# bookHidden: false
# bookCollapseSection: false
# bookComments: false
# bookSearchExclude: false
---

## Scaffold Deploy

### NAME

main.py deploy - 部署系统定时任务

### SYNOPSIS

```bash
main.py deploy <flags>
```

### DESCRIPTION

部署系统定时任务。

```python
Usage: python main.py deploy
______________________________________________________________________
or: python main.py deploy --collector=False         |强制关闭采集器
or: python main.py deploy --collector               |强制开启采集器
or: python main.py deploy --collector --decoupler   |强制开启采集器和订阅解耦器
______________________________________________________________________
```

- 初次部署前先运行 `python main.py entropy --update` 初始化远程队列。
- 命令行参数的优先级高于配置文件。
- 不使用参数启动时，相关配置以配置文件为准。

定时任务包括如下内容：

1. **collector：** 采集器任务（与 `overdue_job` 捆绑）。
2. **decoupler：** 订阅解耦任务，用于清除失效订阅。

需要注意的是，配置文件中设定了默认的 `launch_interval` 任务发起间隔，玩家自定义的间隔数不得小于默认值，否则任务无法部署（或强制调回默认值启动）。

### FLAGS

- collector=COLLECTOR
  - Type: Optional[bool]
  
  - Default: None
  
    强制开启/关闭采集器
  
- decoupler=DECOUPLER
  - Type: Optional[bool]
  
  - Default: None
  
    强制开启/关闭订阅解耦器
