---
Title: Poetry
Author: 邱彼郑楠
Date: 2023-04-03
Modified: 2023-11-02
---

# Poetry
## 安装

根据 [官方文档](https://python-poetry.org/docs/#installation) 中的说明, 在 WSL2(Ubuntu) 系统可通过以下方式进行安装

```shell
curl -sSL https://install.python-poetry.org | python3 -
```

最后可通过 `poetry --version` 查看版本检验安装成功.

## 配置

首先, 列出当前的配置可以使用 `config` 命令的 `--list` 选项, 即 `poetry config --list`.

对于虚拟环境的路径, Poetry 默认将虚拟环境存储在 `{cache-dir}/virtualenvs` 文件夹下. 如果想要将虚拟环境放置在当前项目的根目录中, 需要配置环境变量 `POETRY_VIRTUALENVS_IN_PROJECT` 值为 `true`, 即使用 `config` 命令将 `virtualenvs.in-project` 设置为 `true`.

```shell
poetry config virtualenvs.in-project true
```

## 教程

对于现有的项目, 通过 `poetry init` 命令初始化项目, 根据提示输入初始化设置, `poetry` 会在项目根目录生成 `pyproject.toml` 项目描述文件.

将以下内容添加到项目描述文件 `pyproject.toml` 中, 配置 `poetry` 安装源

```toml
[[tool.poetry.source]]
name = "tsinghua.mirrors"
url = "https://pypi.tuna.tsinghua.edu.cn/simple"
```

使用 `poetry add package_name` 命令将所需要的包添加到 `pyproject.toml` 的 `[[tool.poetry.dependencies]]` 下并安装, 如果想要卸载已安装的包, 则需使用 `poetry remove package_name` 同时 `pyproject.toml` 文件中也会删除.

使用 `poetry shell` 可进入虚拟环境, 在虚拟环境中就可以使用该环境安装的包, 若想退出, 键入 `exit` 即可. 如果不想进入虚拟环境, 则需要使用 `poetry run python file.py` 命令来使用虚拟环境安装的包.

`poetry env use python_release` 可以指定 Python 的解释器并创建对应的虚拟环境.

