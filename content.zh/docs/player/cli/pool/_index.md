---
title: "Scaffold Pool"
weight: 100
# bookFlatSection: false
# bookToc: true
# bookHidden: false
# bookCollapseSection: false
# bookComments: false
# bookSearchExclude: false
---

## Scaffold Pool

### NAME

main.py pool - 订阅池管理

### SYNOPSIS

```bash
main.py pool <flags>
```

### DESCRIPTION

订阅池的命令行管理工具。功能包括：清除 `alive_pool` 中的失效订阅或过期订阅，输出订阅池状态等。

```bash
Usage: python main.py pool
______________________________________________________________________
or: python main.py pool --decouple			|清除失效订阅
or: python main.py pool --overdue			|清除过期订阅
______________________________________________________________________
```

####  `alive_pool` 失效订阅

此处定义的失效指：无法通过ping测试，订阅接口返回值为空或不符合预期。因此，若订阅已“过期”，它显然是“失效”的。

正常状态的订阅接口一般情况下会返回一串 `BASE64` 编码内容，通过编码转换后可解析出节点链接。

####  `alive_pool` 过期订阅

每个采集实例都有一个固定的 `life_cycle` 生命周期（默认24小时），对应着订阅节点的试用时长。

广义上的过期指的是自然时间大于 `life_cycle` ，订阅的生命周期结束，已失效。而此处的“过期”具有更丰富的含义。

采集实例的上下文超级参数 `hyper_params` 中设定了 `threshold` 关键字，默认值为 3（小时），它表示将订阅的生命周期提前/缩短 `threshold` 小时。而系统定时任务中的 `overde_job` 接收的正是计算了此关键字的 `life_cycle`。

设定此关键字的目的可想而知，过期只是某个时刻的概念，只要还没到那个时刻就不会被清除。此时玩家取链接很可能获取到仅剩几秒就（广义）过期的订阅，所以设置此关键词，确保玩家在最恶劣的情况下，仍能取到至少能坚挺 `threshold` 小时的订阅节点。

####  `alive_pool` 订阅池状态

在介绍订阅池状态前需要介绍 `alive action-alias` 的概念。`alive action-alias` 是作者为了降低任务编排难度，为每个可调度的采集实例设定的全局唯一ID，其格式为 `Action[Name]Cloud`，如 `ActionModuCloud` ，对应着一个独立采集实例。

查看订阅池状态，就是查看每个 `alive action-alias` 的剩余数量。若请求成功，可返回如下格式信息：

```powershell
(v2rss-alpha) E:\_GithubProjects\Sources\v2raycs_dev\src>python main.py pool
[2022-01-14 12:06:01] [✓] {'ActionFETVCloud': 3, 'ActionShyNiaCloud': 2, 'ActionCheapCloud': 1, 'ActionAaxCloud': 2}
```

### FLAGS

- overdue=OVERDUE
  - Type: bool
  
  - Default: False
  
    清除过期订阅（decouple 与 overdue 仅能同时执行一项）
  
- decouple=DECOUPLE
  - Type: bool
  
  - Default: False
  
    清除失效订阅（decouple 与 overdue 仅能同时执行一项）
  
- status=STATUS
  - Type: bool
  
  - Default: True
  
    输出订阅池状态（不指定执行参数时默认输出）

