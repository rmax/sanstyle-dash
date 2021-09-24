# 从零开始搭建 AI 环境

````{describe} 软件设置
1. [下载并安装 Anaconda](https://www.anaconda.com/products/individual#Downloads) 开发和管理 [Python](https://www.python.org/) 环境。
2. [下载并安装 Visual Studio Code](https://code.visualstudio.com/) 作为编辑器，并添加 [Python 插件](https://marketplace.visualstudio.com/items?itemName=ms-python.python) 以支持 Python，添加 [Markdown Preview Enhanced](https://marketplace.visualstudio.com/items?itemName=shd101wyy.markdown-preview-enhanced) 以及 [MyST-Markdown](https://marketplace.visualstudio.com/items?itemName=ExecutableBookProject.myst-highlight) 以提供 Markdown 的高级支持。
3. [下载并安装 Git](https://git-scm.com/downloads) 作为项目管理工具。最好选择 {term}`Visual Studio Code` 作为 Git 的编辑器。可以使用 [Git Graph](https://marketplace.visualstudio.com/items?itemName=mhutchie.git-graph) 可视化 Git 管理。
4. （可选）在 Windows 系统安装 {term}`MobaXterm` 以远程操作 Ubuntu 服务器。
````

````{describe} Git 配置
为了正常使用 Git，需要初始化：
```shell
git config --global user.name "Your Name"
git config --global user.email "email@example.com"
```

```{tip} 解决 git@github.com: Permission denied (publickey) 问题
- 客户端生成 ssh key

:::shell
ssh-keygen -t rsa -C "youremail@example.com"
:::

- 把生成的 `id_rsa.pub` 里面的内容复制到你的 github 账号，在 `settings` -->` SSH and GPG keys` 下 `new SSH key`，然后将 `id_rsa.pub` 里的内容复制到 `Key` 中，完成后 `Add SSH Key`。
```
````

## 安装 {term}`Jupyter` Notebook 扩展

[ipython-contrib/jupyter_contrib_nbextensions](https://github.com/ipython-contrib/jupyter_contrib_nbextensions "Jupyter 的各种笔记本扩展的集合") 这个存储库包含了一个扩展集合，可以为 Jupyter 笔记本添加功能。这些扩展大多是用 {term}`JavaScript` 编写的，将在浏览器中本地加载。

IPython-contrib 存储库由一组用户和开发人员独立维护，与 IPython 开发团队没有正式关系。

```shell
pip install jupyter_contrib_nbextensions
jupyter contrib nbextension install --user
jupyter nbextensions_configurator enable --user
pip install autopep8 --user
```

##  Mamba

Conda 作为使用最为广泛的数据科学环境管理工具，可以协助我们很方便的完成创建管理环境、下载安装第三方库、软件包等操作，但其在下载资源的过程中下载速度时常令人捉急，即使使用连接速度更快的国内镜像，也摆脱不了其单线程挨个下载资源导致的低效问题。

而 Mamba（黑曼巴）专为加速Conda而生，其改写了 Conda 下载资源的固有方式，以多线程的方式对网络资源进行并行下载，从而大幅提升 Conda 效率。

首先我们需要安装 Mamba，既然是用来加速 Conda，那么我们可以直接使用下列命令来安装 Mamba：

```shell
conda install -c conda-forge mamba
```

安装完成之后，当你运行 `mamba -V` 查看其版本时会发现返回的是 Conda 的版本信息，这是因为 Mamba 的本质是对 Conda 功能的覆盖，因此我们在使用 Mamba 时其实只要将原有的 Conda 语句中的 conda 替换为 mamba 即可，譬如我们常用的 `mamba clean --all`，即清空本地缓存安装包。