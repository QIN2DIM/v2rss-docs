---
title: "环境复现"
weight: 1
# bookFlatSection: false
# bookToc: true
# bookHidden: false
# bookCollapseSection: false
# bookComments: false
# bookSearchExclude: false
---



# V2RSS 玩家手册

> 更新日期：2021/02/08
>
> 由于开发版（Private）与稳定版（Public）架构相差巨大，本篇文档仅供参考，帮助开发者部署供私人使用的单机项目。

## 环境复现

{{< hint warning >}}

📌 该项目基于 Windows 开发测试，基于Linux 调试部署，Mac 用户可能无法正常使用。

{{< /hint  >}}

{{< hint info >}}

📌 v5.u.r.beta 版本项目仍基于 Python 开发，暂未涉及 Go，也即本项目大部分高级功能暂未开源。

{{< /hint  >}}

|      项目名       |                 参考软件                 |          备注          |
| :---------------: | :--------------------------------------: | :--------------------: |
|     操作系统      |         Windows 家庭版 ，CentOS7         |           /            |
|     开发工具      | Pycharm 2019.3.3 专业版  ，Goland 20.3.1 | Python3.8 ，Go 1.17.2  |
|    数据库管理     | RedisManagerDesktop ，Navicat Premium 15 |           /            |
|     远程登录      |         Finalshell ，Xshell/Xftp         |           /            |
|     开发依赖      |      Google Chrome ， ChromeDriver       |           /            |
| 辅助工具（Win64） |            Anaconda Navigator            |           /            |
| 辅助工具（Linux） |               pyenv，tmux                | 便于版本管理与项目调试 |

