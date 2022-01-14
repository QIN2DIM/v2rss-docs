---
title: "Scaffold Build"
weight: 10
# bookFlatSection: false
# bookToc: true
# bookHidden: false
# bookCollapseSection: false
# bookComments: false
# bookSearchExclude: false
---

## Scaffold Build

### NAME

在 Ubuntu 白环境下构建运行环境。建议在 `Ubuntu 18.04 TLS` 或 `Ubuntu 20.04 TLS` 中使用。

### SYNOPSIS

```bash
main.py build <flags>
```

### DESCRIPTION

构建内容如下：

1. 执行脚本 `apt-get update && apt-get install -y gcc wget unzip` 更新源并拉取脚本运行所需依赖

2. 检查 `google-chrome` 状态，若不存在则安装拉取最新稳定版 `google-chrome` 并返回版本号，若存在则直接返回当前客户端的版本号。

   若指定了 `force ` 参数，本机已存在 `google-chrome` 时会卸载重装。

3. 安装 `chromedriver`，根据 `google-chrome` 版本匹配相应版本的驱动。
4. 移动 `chromdriver` 至指定目录下，并赋予 `u+x` 权限。
5. 清理运行缓存（若权限不足则跳过）。清理安装包和下载缓存，清屏。

### FLAGS

- force=FORCE

  - Type: Optional[bool]

  - Default: None

    若指定该参数，则当环境中已存在 google-chrome 时卸载重装。



