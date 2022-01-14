---
title: "Scaffold Server"
weight: 320
# bookFlatSection: false
# bookToc: true
# bookHidden: false
# bookCollapseSection: false
# bookComments: false
# bookSearchExclude: false
---

## Scaffold Server

### NAME

main.py server - ``PRODUCTION`` 接口服务器（仅在linux部署时生效）

### SYNOPSYS

```bash
main.py server <flags>
```

### DESCRIPTION

{{< expand"查看接口文档" >}}

点此 [查看接口文档](https://www.apifox.cn/apidoc/shared-fe514493-d572-461f-894e-8a39375cef05)，访问密码：y2WZHeHF

{{< /expand >}}

脚手架基础用法如下：

```python
Usage: python main.py server
______________________________________________________________________
or: python main.py server --host=127.0.0.1 --port=22332   |指定端口运行
or: python main.py server --detach=False                  |订阅耦合
______________________________________________________________________
```

{{< hint info>}}

📌 为了在生产环境下获得最佳性能，默认禁用 ``debug`` 和 ``access_log``。

{{< /hint >}}

{{< hint info>}}

📌 `Sanic` 可指定  `workers` 充分利用多核性能，也可直接指定 `--fast` 参数直接拉满，子进程间可以负载均衡。而云彩姬服务端口仅供个人使用，不存在高并发的应用场景，也即 `workers=1` 既可（默认），无需更改指定，徒增功耗。

{{< /hint >}}

{{< hint warning>}}

📌 通过此指令直接运行的是生产服务器，若要运行开发环境调试代码，请手动运行 `examples/server_dev.py` 或 ``src/services/app/server``。

{{< /hint >}}

### FLAGS

- host=HOST

  - Type: Optional[str]
  - Default: None 

- port=PORT

  - Type: Optional[int]
  - Default: None

- detach=DETACH

  - Type: Optional[bool]

  - Default: None

    分离订阅（不指定时默认为 True）。若 `detach is True`，通过接口层申请的订阅才会被系统删除。 意味着在接口调试时，指定 ``detach=False`` 被请求的链接不会被删除。
