---
title: "Scaffold Synergy"
weight: 310
# bookFlatSection: false
# bookToc: true
# bookHidden: false
# bookCollapseSection: false
# bookComments: false
# bookSearchExclude: false
---
## Scaffold Synergy

### NAME

main.py synergy - 部署协同工作节点

### SYNOPSIS

```bash
main.py synergy -
```

### DESCRIPTION

#### INTRO

在介绍 `协同工作` 的概念前，需要先了解以下与之相关的背景知识。

在采集实例上下文超级参数 `hyper_params` 中设定了 `aff` 和 `synergy` 两个关键字。

- aff=AFF
  - Type:Optional[int]
  - Default:0
  - 协同机拷贝数
- synergy=SYNERGY
  - TypeOptional[bool]
  - Default:False
  - 协同模式/采集模式上下文切换

#### AFF

`aff` 凭借提供商“佣金返利”的商业模式，携带被增益订阅的邀请链接进行多对一的协同注册，简单实现被增益订阅可用流量的拔升。每个提供商的“返利”规则大有不同，账户邀请链接数和增益流量大相径庭。

因此，并不是任何一个采集实例都可以设定 `aff` 参数，也并不是所有可以设定 `aff` 参数的采集实例都值得被增益，部分规则的返利流量实在太少，相对的采集成本较大，在拥有性价比更高的选择时，可以忽略。

显然的，`aff` 的设定需要遵循规则，其因该是一个大于零的自然数，且不应多于规则限制的可邀请数量。在最佳实践中，`aff∈[1,10]` 这在源码中也加以限制，当玩家设定的 `aff` 超乎预期时，协同实例的拷贝逻辑将失效。

#### SYNERGY

由上文可知，当采集实例正常结束前，会进行 `aff` 超级参数的解析，若含义有效，则会拷贝 `aff` 个切换至协同模式的实例通过 `MessageQueue(RedisClient)` 广播至订阅频道。需要注意的是，这个广播出去的信息是一个完整的（处于协同模式的）运行实例对象的「上下文摘要」，监听此频道的 `synergy` 服务节点都可以正常过滤解析这些字段，并通过一系列逻辑将摘要信息恢复成实例运行所需的各项参数，最后执行协同注册任务。

#### SYNERGY PATTERN

到了正式介绍 `协同工作` 模式的时候了。使用如下指令可拉起一个协同工作进程，显然地，它不需要任何脚手架参数。

```bash
python main.py synergy
```

- `synergy pattern` 的指令逻辑被精简优化，可部署到任意的物理机上，甚至一台物理机可以部署多个 `synergy` 服务节点。

- 处于 `协同模式` 的服务节点几乎只做三件事： 接受 `aff` 上下文信息，恢复现场，执行协同注册任务。

- `synergy_node` 基于 `APScheduler` 运行，节点宕机可被自动拉起恢复工作。
- 处于 `协同模式` 的服务节点可以长期工作。只要核心业务代码不做升级，`synergy_node`可以一直运行下去，如上文所说，`synergy_node`可以正常解码任务信息并执行指定任务，无论我们再怎么更新采集队列，变换队列容量或属性，甚至拓展采集器的业务逻辑，只要不改动上下文摘要的“通信协议头”，`synergy_node`就能不停机地一直工作下去（若协议头不匹配，会把无法解析的消息当成杂质过滤掉）。

