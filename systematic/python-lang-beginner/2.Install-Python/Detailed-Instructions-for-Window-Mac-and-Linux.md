# 适用于 Windows、Mac 和 Linux 的详细说明<!-- omit in toc -->

- [1. 在 Windows 上安装 Python](#1-在-windows-上安装-python)
- [2. 在 MacOS 上安装](#2-在-macos-上安装)
- [3. 在 Linux 上安装 Python](#3-在-linux-上安装-python)

## 1. 在 Windows 上安装 Python

1. 使用 Microsoft Store： Microsoft 在 Microsoft Store 中发布了 Python 3 的社区版本。这是在 Windows 上安装 Python 的推荐方法，因为它可以自动处理更新，并且也可以轻松卸载。
2. 使用官方安装程序： 从 [Python 官方下载网站](https://www.python.org/downloads/) 下载 Python 安装程序。此方法不会自动更新。使用此安装程序时，请确保选中 “将 Python 添加到 PATH” 复选框。
3. WSL 内部： 需要安装 WSL 本身，之后按照下面的 Linux 安装说明进行操作。

## 2. 在 MacOS 上安装

暂略

## 3. 在 Linux 上安装 Python

检查已安装的内容：

```shell
# Python 2
python --version

# Python 3
python3 --version
```

使用包管理器安装：

```shell
# Ubuntu、Linux Mint 或 Debian
# 这还会安装一个名为 python-is-python3 的包，使命令 python 指向 python3。相信我，这会为你省去很多麻烦。
apt install python3 python-is-python3
```
