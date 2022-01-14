---
title: "Overview"
weight: 1
# bookFlatSection: false
# bookToc: true
# bookHidden: false
# bookCollapseSection: false
# bookComments: false
# bookSearchExclude: false
---

# V2RSS 脚手架指令

## 基础指令

<!-- weight:5~99-->

{{< columns >}} <!-- begin columns block -->

### [scaffold ping](/docs/player/cli/ping)

<!-- weight:5-->

测试 Redis 数据库连接。

<---> <!-- magic separator, between columns -->

### [scaffold build](/docs/player/cli/build)

<!-- weight:10-->

在 Ubuntu 中构建基础运行环境。

 {{< /columns >}}

## 订阅管理

<!-- weight:100~200-->

{{< columns >}} <!-- begin columns block -->

### [scaffold pool](/docs/player/cli/pool)

<!-- weight:100-->

订阅池的命令行管理工具。功能包括：剔除 `alive_pool` 中的失效订阅或过期订阅，输出订阅池状态等。

<---> <!-- magic separator, between columns -->

 {{< /columns >}}

## 系统任务

<!-- weight:300~400-->

{{< columns >}}

### [scaffold deploy](/docs/player/cli/deploy)

<!-- weight:300-->

部署定时任务节点。

<--->

### [scaffold synergy](/docs/player/cli/snergy)

<!-- weight:310-->

部署协同工作节点。

{{< /columns >}}

{{< columns >}} <!-- begin columns block -->

### [scaffold server](/docs/player/cli/server)

<!-- weight:320-->

部署 `PRODUCTION` 接口服务器。

<---> <!-- magic separator, between columns -->

### [scaffold entropy](/docs/player/cli/entropy)

<!-- weight:330-->

采集队列的命令行管理工具。功能包括：更新待办任务、更新采集队列容量，检查待办任务心跳，输出采集队列摘要信息。

{{< /columns >}} 

## 高级指令

<!-- weight:500~600-->

{{< columns >}} <!-- begin columns block -->

### [scaffold mining](/docs/player/cli/mining)

<!-- weight:500-->

采集、清洗、分类、存储暴露在公网上的 SSPanel-Uim 站点。

<---> <!-- magic separator, between columns -->

### [scaffold spawn](/docs/player/cli/spawn)

<!-- weight:510-->

释放所有本机采集实例，基于 gevent 并发执行。

{{< /columns >}}

## 实验功能

<!-- weight:1000+-->

{{< columns >}} <!-- begin columns block -->

### [scaffold ash](/docs/player/cli/ash)

<!-- weight:1000-->

通过设定的 `threshold` 审查订阅池，清洗出各类订阅中的优质节点，重新排列组合生成可被 Clash 吸收的规则的 `config.yaml` ；自动打开 Clash 导入配置文件。

<---> <!-- magic separator, between columns -->

 {{< /columns >}}
