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

{{< columns >}} <!-- begin columns block -->

## [scaffold ping](/docs/player/cli/ping)

测试数据库连接。这是个不常用的功能，仅会在新环境首次创建时使用，如在 GitHub Actions 中检查配置是否正确。

<---> <!-- magic separator, between columns -->

## [scaffold decouple](/docs/player/cli/decouple)

剔除 live 订阅池中的失效链接。

 {{< /columns >}}

{{< columns >}} <!-- begin columns block -->

## [scaffold overdue](/docs/player/cli/overdue)

剔除 live 订阅池中的过时链接。

<---> <!-- magic separator, between columns -->

## [scaffold remain](/docs/player/cli/remain)

打印 live 订阅池的运行状态，所含信息包括「订阅源」的存活数量，类型以及别名。

 {{< /columns >}}

{{< columns >}} <!-- begin columns block -->

## [scaffold parse](/docs/player/cli/parse)

内置的订阅解析工具。完成订阅链接--节点分享链接--节点服务器明文信息的正反向解析工作。

<---> <!-- magic separator, between columns -->

## [scaffold build](/docs/player/cli/build)

构建运行环境。这是个不常用的功能，仅会在服务首次部署时使用，如在 GitHub Actions 中拉取缺失的第三方依赖。

 {{< /columns >}}

{{< columns >}} <!-- begin columns block -->

## [scaffold spawn](/docs/player/cli/spawn)

一次性清空并执行本机所有采集实例。任务基于 gevent 并发执行，运行功率取决于队列大小以及本机硬件性能。

<---> <!-- magic separator, between columns -->

## [scaffold server](/docs/player/cli/server)

部署调试服务，挂载可用的定时任务，并部署 flask 请求中转服务。任何可启动的项目都可通过配置文件精准调控。

 {{< /columns >}}

{{< columns >}} <!-- begin columns block -->

## [scaffold mining](/docs/player/cli/mining)

采集、清洗、分类、存储暴露在公网上的 SSPanel-Uim 站点。少数情况下可用于扫描不携带 staff statement footer 的分类站点。

<---> <!-- magic separator, between columns -->

## [scaffold entropy](/docs/player/cli/entropy)

在控制台输出本机采集队列的抽象信息。包含的字段有存活周期，源链接以及采集类型。

 {{< /columns >}}

{{< columns >}} <!-- begin columns block -->

## [scaffold ash](/docs/player/cli/ash)

「实验功能」 内置的 Clash for Windows 订阅拉取组件，可实现代理节点的一键采集，清洗，转换与自动导入。 

<---> <!-- magic separator, between columns -->

## [scaffold panel](/docs/player/cli/panel)

「实验功能」唤起由 Easygui 编写的仪表盘工具箱。

 {{< /columns >}}

