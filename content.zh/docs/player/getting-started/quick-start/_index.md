---
title: "快速上手"
weight: 10
# bookFlatSection: false
# bookToc: true
# bookHidden: false
# bookCollapseSection: false
# bookComments: false
# bookSearchExclude: false
---

# 快速上手

快速部署一个可以采集订阅的 V2RSS 后端服务。

{{< tabs >}}
{{< tab "Linux(Ubuntu)" >}} 

{{< hint info>}}

📌 不建议使用国内厂商提供的 VPS 运行本项目。

{{< /hint >}}

{{< hint warning>}}

📌 脚手架 build 脚本仅能在 Ubuntu 下运行。

📌 系统服务是阻塞运行的，需要使用类似 `tmux` 之类的会话管理工具，否则连接断开后服务进程会被释放。

{{< /hint >}}

1. **Fork 项目，拉取源码**

```bash
git clone https://github.com/QIN2DIM/V2RayCloudSpider.git /home/v2rss-alpha
```

2. **进入工作目录**

```bash
cd /home/v2rss-alpha/V2RaycSpider1225
```

3. **拉取必要依赖**

   根据你的情况选择 `pip/pip3` ，或使用 `pyenv/conda` 。

```bash
pip install -r ./requirements.txt
```

4. **初始化组织结构以及配置文件**

```bash
cd src && python3 main.py build
```

5. **再次执行，构建基础运行环境**

   脚本构建的具体内容可参考 [build](/docs/player/cli/build) 脚手架指令

```bash
python3 main.py build
```

6. **修改配置文件**

   打开位于 `/home/v2rss-alpha/V2RaycSpider1225/src` 目录下的 `config.yaml`，根据行内注释配置全局变量 `REDIS_NODE`，以及 `POOL_CAP`。其中 `REDIS_NODE` 需要玩家架设一个**可远程访问的** Redis 节点。

7. **测试连接**

   若返回 `欢迎使用` 字样说明配置文件编写以及节点配置都没问题，可以正常运行项目了。

```bash
python3 main.py ping 
```

8. **初始化服务对象**

```bash
# Create Remote EntropyHeap Object.
python3 main.py entropy --update

# Set Unified Pool Capacity.
python3 main.py entropy --cap=8
```

9. **试运行采集器**

```bash
cd /home/v2rss-alpha/V2RaycSpider1225 && python3 examples/atomic_go.py
```

若出现类似如下的日志信息，说明驱动器配置正确，可以部署服务了。

```bash
2022-01-14 14:52:50 | DEBUG - >> RUN [ActionMaSaiKeCloud] - params={'aff': 5, 'threshold': 3}
2022-01-14 14:52:56 | SUCCESS - >> STORE [ActionMaSaiKeCloud] - subscribe_url=https://ma.sai.ke?sub=3
```

10. **部署系统服务**

{{< hint info>}}

📌 如下三个系统服务均为独立的阻塞进程，如果都要在同一台物理机上部署，需要开启多个会话窗格操作。

📌 可在「[脚手架指令](/docs/player/cli/overview)」查看关于 `deploy` ，`synergy` 以及 `server` 的详细介绍。

{{< /hint >}}

```bash
# 部署系统 任务
cd /home/v2rss-alpha/V2RaycSpider1225/src && python3 main.py deploy

# 部署协同工作节点
cd /home/v2rss-alpha/V2RaycSpider1225/src && python3 main.py synergy

# 部署 PRODUCTION 接口服务器
cd /home/v2rss-alpha/V2RaycSpider1225/src && python3 main.py server --host=0.0.0.0 --port=22333
```

{{< /tab >}}
{{< tab "Windows" >}} 





{{< /tab >}}

{{< /tabs >}}

