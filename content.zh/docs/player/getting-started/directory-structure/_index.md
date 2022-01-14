---
title: "目录结构"
weight: 40
# bookFlatSection: false
# bookToc: true
# bookHidden: false
# bookCollapseSection: false
# bookComments: false
# bookSearchExclude: false
---

# 目录结构

## New Project Scaffolding

若玩家直接使用 `git` 指令拉取源码仓库，那仅需关注其中的 `V2RaycSpider[KernelCode]` 文件夹，如下目录结构以此为根展开介绍。

 ```asp
 .
 ├── examples
 │   ├── __init__.py
 │   ├── atomic_assault.py
 │   ├── atomic_check.py
 │   ├── atomic_go.py
 │   └── server_dev.py
 ├── src
 │   ├── apis
 │   ├── database
 │   ├── driver
 │   ├── services
 │   ├── __init__.py
 │   ├── config.py
 │   ├── config.yaml
 │   ├── config-sample.yaml
 │   └── main.py
 └── requirements.txt
 ```

## Directory Structure Explained

### examples

这里存放一些精简化的后端功能接口，玩家可通过这些运行案例迅速了解服务间的层级关系以及核心业务的实现逻辑。其中，`server_dev.py` 启动的一个 `dev` 环境的接口服务器；`atomic_go.py` 启动一个指定的采集实例，可通过修改 `alias` 指定不同的采集实例；`atomic_assault.py` 则是实例运行的 `gevent` 版本，可并发地执行多个采集实例；`atomic_check.py` 用于检查本地采集队列的健康状态。

值得一提的是，这些功能都可通过脚手架快速调用，放在这主要便于扁平化的案例介绍。

### src/apis

存放全局接口函数，如一些复杂的脚手架接口逻辑会在此编排。

### src/database

存放系统运行缓存。在项目初始化后，此文件夹被自动创建。

### src/driver

存放 `chromedriver` 驱动程序。在项目初始化后，此文件夹被自动创建。

### src/services

存放核心业务代码，包括如下内容：

```
.
├── app
│   ├── bot
│   ├── panel
│   ├── server
│   └── __init__.py
├── collector
│   ├── nest
│   ├── __init__.py
│   ├── actions.py
│   ├── core.py
│   ├── exceptions.py
│   └── operator.py
├── decoupler
│   ├── __init__.py
│   └── decoupler.py
├── middleware
│   ├── __init__.py
│   ├── stream_io.py
│   ├── subscribe_io.py
│   └── workers_io.py
├── utils
│   ├── accelerator
│   ├── armor
│   ├── sspanel_mining
│   ├── toolbox
│   └── __init__.py
├── __init__.py
├── deploy.py
├── scaffold.py
└── settings.py
```

- app

  存放接口服务器模型。可见，目前云彩姬支持以聊天机器人（Nonebot、Telegram-bot、DingTalk-bot......）、PC客户端面板、以及API接口的形式分发订阅。

- collector

  采集器逻辑层代码。`core.py` 存放核心业务代码，包含采集器整个周期的行为函数；`actions.py` 维护一个  `__entropy__` 本地采集队列，存放着采集实例的上下文摘要信息；`operator.py` 存放着一个接口解释器，输入 `atomic_context` ，输出一个特征完整的采集实例；`exceptions.py` 存放采集器运行时常见的报错类型。

- decoupler

  订阅解耦器，核心功能是清楚失效订阅。

- middleware

  数据库交互层。`stream_io.py` 存放各类型数据库的基准链接方案；`subscribe_io.py` 存放着继承自 `RedisClient` 基类的高级逻辑代码，负责管理订阅池；`workers_io.py` 存放着继承自 `RedisClient` 基类的高级逻辑代码，包含任务堆管理，消息队列，访问控制等模块。

- utils

  可移植模组。存放着云彩姬生态的可移植模组，包含 `accelerator` 协程加速组件，云彩姬后端服务是基于协程运转的，此组件基于 Gevent 构建了一个可管理的极其轻量的并发框架；`armor` 存放着一系列人机对抗组件，通过适配器接口无缝衔接至采集器的生命周期中；`sspanel_mining` 是项目 [RobAI-Lab](https://github.com/RobAI-Lab)/**[sspanel-mining](https://github.com/RobAI-Lab/sspanel-mining)** 的兼容版本，可通过脚手架 `mining` 指令运行；`toolbox` 存放着若干个工具类函数，包括构建基础环境的 `build` 脚本，`InitLog` 自定义日志，`SubscribeParser` 订阅解析，以及包含着各种常用功能的`ToolBox`工具箱。

- deploy.py

  系统任务的调度中心。

- scaffold.py

  脚手架源码。

- settings.py

  系统设置。设定全局变量用于精确的绝对路径定位，初始化系统日志，引用 `src/config.py` 中的配置信息。 

### src/config.yaml

项目配置文件。在项目初始化后，从 `src/config_sample.yaml` 拷贝生成。 `src/config.py` 的功能是读取配置信息并转义成 Python 全局变量。

关于配置文件的具体介绍可见「[CONFIGURATION](/docs/player/getting-started/configuration)」。

### src/main.py

脚手架入口文件，作为运行根辐射系统指令，在脚手架未编译前，作为系统指令的统一入口。
