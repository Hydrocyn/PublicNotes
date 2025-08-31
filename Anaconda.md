---
tags:
  - Python
  - MachineLearning
---
[Anaconda | The World’s Most Popular Data Science Platform](https://www.anaconda.com/)
版本更新文档：[Anaconda release notes — Anaconda documentation](https://docs.anaconda.com/anaconda/release-notes/) 

Anaconda 是一个开源的、用于科学计算的 Python 和 R 语言的发行版。它包含了一系列常用的科学计算和数据分析库，包括 NumPy、SciPy、Pandas、Matplotlib 和 Scikit-learn，使得安装、管理和切换不同版本的库变得更加方便。Anaconda 不仅仅是 Python 的发行版，还提供了一个名为 conda 的包管理器，能够帮助用户创建、导出、安装和更新环境。

#### python 与发行版本解惑

[可能是最全的 Python 环境管理工具对比 - 知乎](https://zhuanlan.zhihu.com/p/681222081) 

Difference between conda and pip
	[Anaconda | Understanding Conda and Pip](https://www.anaconda.com/blog/understanding-conda-and-pip)
	[请问大神们，pip install 和conda install有什么区别吗？ - 知乎 (zhihu.com)](https://www.zhihu.com/question/395145313)
	[工具篇：conda and pip - 知乎](https://zhuanlan.zhihu.com/p/508506160)
	[anaconda探究：pip与conda安装异同_conda装包会装很多依赖而pip不会_我是最帅的~的博客-CSDN博客](https://blog.csdn.net/qq_26129959/article/details/90110123#:~:text=1.pip%E5%AE%89%E8%A3%85%E4%B8%8D%E4%BC%9A%E5%AE%89%E8%A3%85%E6%89%80%E6%9C%89%E7%9A%84%E4%BE%9D%E8%B5%96%E9%A1%B9%E5%8F%AA%E4%BC%9A%E5%AE%89%E8%A3%85%E9%83%A8%E5%88%86%E4%BE%9D%E8%B5%96%E9%A1%B9%EF%BC%8C%E8%80%8Cconda%E4%BC%9A%E5%AE%89%E8%A3%85%E5%85%A8%E9%83%A8%EF%BC%9B%202.pip%E4%B8%8Econda%E4%B8%8D%E4%BC%9A%E9%87%8D%E5%A4%8D%E5%AE%89%E8%A3%85%E5%B7%B2%E7%BB%8F%E5%AE%89%E8%A3%85%E7%9A%84%E4%BE%9D%E8%B5%96%E3%80%82,3.pip%E4%B8%8D%E4%BC%9A%E5%91%8A%E8%AF%89%E4%BD%A0%E9%83%BD%E5%AE%89%E8%A3%85%E4%BA%86%E4%BB%80%E4%B9%88%EF%BC%8Cconda%E4%BC%9A%204.pip%E5%AE%89%E8%A3%85%E7%9A%84%E5%86%85%E5%AE%B9%E4%B8%8D%E4%BC%9A%E6%98%BE%E7%A4%BA%E5%9C%A8anaconda%20navigation%E7%9A%84%E7%8E%AF%E5%A2%83%E4%B8%AD%EF%BC%8Cconda%E4%BC%9A%E3%80%82)

Anaconda 包含 Python 解释器，但它是一个更大的科学计算工具包，旨在简化库和环境的管理。你可以通过 conda 创建虚拟环境，使得你能够在不同项目中使用不同版本的 Python 和库。

何时需要单独安装 python：
- 使用特定版本的 Python：某些库或工具可能需要使用特定版本的 Python 才能正常工作。在这种情况下，您可能需要单独安装 Python 的所需版本。
- 使用 Anaconda 中不可用的包：如果您需要使用 Anaconda 中不可用的包，则需要单独安装 Python 并使用 pip 或 Conda 安装这些包。
- 管理 Python 环境：如果您需要管理多个 Python 环境用于不同的项目，则最好单独安装 Python 并使用虚拟环境工具，如 virtualenv 或 conda environments。
- 使用系统默认 Python：在某些情况下，您可能需要使用系统默认的 Python 解释器。在这种情况下，您需要单独安装 Python 并将其设置为系统默认值。

让我们以 Python 为例，说明发行版本和不同版本之间的区别：
1.	官方 CPython： 这是 Python 的官方实现，由 Python Software Foundation 提供。它是最常用的 Python 版本，支持各种平台。你可以从 Python 官方网站获取官方 CPython 的最新版本。
2.	Anaconda Python： Anaconda 是一个用于科学计算的 Python 发行版，它包含了许多常用的科学计算库。Anaconda 还提供了 conda 包管理器，用于方便地安装、更新和管理库和环境。
3.	Jython： 这是一个将 Python 代码运行在 Java 虚拟机上的实现。它允许 Python 代码与 Java 代码互操作。
4.	IronPython： 这是一个将 Python 代码运行在 .NET 框架上的实现。它与 .NET 平台集成，允许 Python 与 C# 等语言进行交互。

关于不同版本之间的区别：
1.	语法和功能： 新版本通常会引入新的语法特性和功能。这些变化可能是为了提高语言的性能、简化语法或引入新的编程范式。
2.	性能： 一些版本可能对性能进行了优化，包括解释器性能、库的性能改进等。
3.	库和模块： 不同版本可能包含不同的标准库和第三方库。某些库可能只支持特定的 Python 版本。
4.	安全性和稳定性： 更新的版本通常包含对安全漏洞的修复和一些改进，以提高语言的稳定性。

C 语言并没有像 Python 那样的”发行版本”的概念。C 语言是一种标准化的编程语言，其标准由国际标准化组织（ISO）和国际电工委员会（IEC）制定。因此，C 语言的不同实现都应该遵循相同的标准，以确保代码的可移植性。
然而，有一些流行的 C 语言编译器，例如：
	1.	GCC（GNU Compiler Collection）： 这是一个包含 C、C++、Fortran 等语言编译器的集合，是开源社区广泛使用的工具。
	2.	Clang： 由 LLVM 项目开发的另一个流行的编译器，用于支持多种编程语言。
这些编译器通常实现了 C 语言的标准，并提供了一些额外的功能和优化。

### cache

pytorch 处理：
基础内容补充：[新手如何入门PyTorch，了解它跟 TensorFlow的区别！ - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/196526402) [Pytorch 最全入门介绍，Pytorch入门看这一篇就够了-CSDN博客](https://blog.csdn.net/Python84310366/article/details/132106943) 
[手把手带你入门深度学习（一）：保姆级Anaconda和PyTorch环境配置指南_anaconda和pytorch的关系-CSDN博客](https://blog.csdn.net/qq_36306288/article/details/128484260)

存在的问题：
vscode 右下角显示的解释器似乎跟虚拟环境有所不同
	代码里的报错显示跟解释器的设置有关，但是运行代码时，似乎没有什么关系（应该是有关系，可以初始 python 解释器环境里也有 numpy 包）？

vscode 的 conda 终端不显示环境名，没搞懂到底是什么原因 (可能是 conda 在终端的初始化没有做好）。powershell 和 cmd 在这个终端到底有什么区别，这是我自己选的吗 ([VSCode 中切换默认终端（PowerShell、CMD、WSL等） - 呓雫 - 博客园](https://www.cnblogs.com/leileigwl/p/18247874))（每一行开头的 PS 应该就是 powershell 的意思 [VSCode 集成终端 | 菜鸟教程](https://www.runoob.com/vscode/vscode-terminal.html) ）？ [解决vscode终端不显示conda环境变量名称问题【详细步骤！实测可行！！】_vscode终端不显示虚拟环境名称-CSDN博客](https://blog.csdn.net/xiaoh_7/article/details/139465137) 

初始化 conda
```bash
# 对于 PowerShell
conda init powershell
# 对于 CMD
conda init cmd.exe
# 对于 Bash (Linux/macOS)
conda init bash
```


### 安装 anaconda

anaconda 安装指导：
[VSCode + Anaconda（Python）开发环境搭建 - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/88458083)
[安装Anaconda3以及配置环境变量 - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/382980557) 
[Anaconda安装与Python环境搭建（不看后悔版） - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/511233749) 

卸载工具：[Uninstalling Anaconda Distribution — Anaconda documentation](https://docs.anaconda.com/anaconda/uninstall/)

Anaconda 版本和 Python 版本存在对应关系，同一个 Anaconda 可以支持多个 Python 版本

**是否将 Anaconda 添加到系统环境变量中**, **Add Anaconda to PATH**
在安装过程中，你可以选择是否将 Anaconda 添加到系统环境变量中。建议选择此选项，以便在命令行中直接使用 conda 命令
>如果勾选会影响其他程序的使用，大概是因为命令行会找到 anaconda 环境下的 python 进行使用
1. 如果你还没有安装 Python：建议勾选此选项。这将自动将 Anaconda 添加到系统环境变量，使你可以在命令行或终端中直接运行 Anaconda 及其包含的 Python。这可以简化你的工作流程，并减少以后手动配置环境变量的需要。
2. 如果你已经安装了Python：不建议勾选此选项。原因是勾选此选项可能会更改你当前的默认Python版本为Anaconda自带的Python版本。这可能会影响到你其他依赖于特定Python版本的程序或库。如果你希望在命令行中使用原来的Python版本，那么不勾选此选项是更好的选择。
3. 无论你是否勾选，都可以手动配置环境变量：如果你没有勾选“添加到环境变量”，或者出于某种原因需要更改环境变量的设置，你可以手动进行配置。这通常涉及到编辑系统的环境变量设置，将Anaconda的路径添加到其中。虽然这需要一些额外的步骤，但它给了你更多的灵活性和控制力。
4. 如何测试环境变量是否设置成功：安装完成后，你可以打开Anaconda Prompt窗口，输入`conda --v`来检测Anaconda是否安装成功。如果返回了Anaconda的版本信息，说明安装成功。另外，输入`conda info --envs`可以查看当前所安装的环境变量。

完成安装后，你可以在系统中找到 Anaconda Navigator（一个可视化的管理工具）以及 Anaconda Prompt（命令行工具）

打开 Anaconda Navigator 或 Anaconda Prompt。
	•	在 Anaconda Prompt 中，输入 `conda list`，检查已安装的包列表。这将显示安装的 Python 和其他库的版本信息。


## 虚拟环境

### 虚拟环境概念剖析

虚拟环境（Virtual Environment）是在 Python 中用于隔离项目环境和依赖的工具。通过创建虚拟环境，可以在同一系统中的不同项目中使用不同的 Python 版本和库，而不会互相干扰。

- Isolation（隔离）：虚拟环境的核心概念是隔离项目的 Python 运行环境，使其与系统的全局 Python 环境独立开来。
- 项目依赖： 虚拟环境允许你在每个项目中指定独立的依赖，确保项目的依赖不会与其他项目冲突。
- 版本管理： 虚拟环境使得你能够轻松地在不同项目中使用不同的 Python 版本。

使用虚拟环境的优势：
1. 隔离项目环境： 虚拟环境允许你在项目之间创建独立的环境，每个环境都有自己的Python解释器和库。这样可以防止项目之间的冲突和版本不一致性。
2. 版本控制： 通过虚拟环境，你可以轻松切换和管理Python的不同版本，确保项目在指定的Python版本下运行。
3. 依赖管理： 可以在每个虚拟环境中安装和管理项目所需的依赖库，而不会影响全局Python环境。

在Python中，有几种工具可以用来创建和管理虚拟环境，其中两个主要的工具是：
- venv： 是 Python 标准库中包含的一个虚拟环境管理工具，使用 `python -m venv myenv` 创建虚拟环境
- Conda： 是 Anaconda 发行版提供的一个包管理工具，它不仅可以管理 Python 库，还可以创建和管理虚拟环境。可以使用 `conda create --name myenv` 创建 Conda 虚拟环境

[Python版本管理器之Pyenv-win介绍与安装-CSDN博客](https://blog.csdn.net/yuanjinshenglife/article/details/145670991) 
[pyenv-win/pyenv-win: pyenv for Windows. pyenv is a simple python version management tool. It lets you easily switch between multiple versions of Python. It's simple, unobtrusive, and follows the UNIX tradition of single-purpose tools that do one thing well.](https://github.com/pyenv-win/pyenv-win) 
[pyenv-win+venv配置不同python版本和虚拟环境_pyenv-win-venv-CSDN博客](https://blog.csdn.net/EstrangedZ/article/details/145733886) 

### 创建虚拟环境

创建虚拟环境
```bash
conda create --name myenv python=3.9
```

#### 指定虚拟环境的安装路径：不安装在 C 盘

- 为什么虚拟环境默认安装在 C 盘？如何修改路径？
默认情况下，Conda 会将虚拟环境存储在用户目录下的 `.conda\envs` 文件夹中（例如 `C:\Users\你的用户名\.conda\envs`）。这是为了确保权限管理和用户隔离的便捷性。
但如果你希望将虚拟环境安装到其他磁盘（如 D 盘、E 盘），可以通过以下两种方法实现：

**方法 1：创建环境时手动指定路径**
每次创建环境时，通过 `--prefix` 参数直接指定目标路径，完全绕过默认位置。
1. 打开 Anaconda Prompt 或普通命令提示符。
2. 输入以下命令（以安装到 D 盘为例）：
`conda create --prefix D:\conda_envs\myenv python=3.9` 
（对比不指定位置的指令 `conda create --name myenv python=3.9`）
>`D:\conda_envs\myenv` 是自定义的路径，需提前创建好父目录（如 `D:\conda_envs`）。
3. 激活环境时需指定完整路径：`conda activate D:\conda_envs\myenv`


**方法 2：永久修改 Conda 的默认环境路径**
通过修改 Conda 的配置文件 `.condarc`，设置新的默认虚拟环境存储路径。

1. 找到或创建 `.condarc` 文件：
    - 默认路径：`C:\Users\你的用户名\.condarc`。
    - 如果不存在，可以通过此命令生成：`conda config --set show_channel_urls yes`
2. 编辑 `.condarc` 文件：  
    用文本编辑器（如 Notepad++、VS Code）打开 `.condarc`，添加以下内容：
```
envs_dirs:
	- D:\conda_envs  # 你的自定义路径（需提前创建）
	- C:\Users\你的用户名\.conda\envs  # 保留原路径作为备选
```
Conda 会按列表顺序优先使用第一个路径。如果 `D:\conda_envs` 不可用（如权限不足），则会自动使用第二个路径。
也可以手动添加：`conda config --add envs_dirs G:/conda_envs`
3. 验证配置生效：`conda config --show envs_dirs`，应显示你设置的路径列表。
4. 创建新环境测试：`conda create --name myenv python=3.9`，此时环境会默认安装到 `D:\conda_envs\myenv`
5. 激活环境（无需指定路径）：`conda activate myenv`

**检查环境位置**：`conda env list`

>Anaconda 所在的文件夹似乎自带一个环境文件夹 `G:\anaconda3\envs`，新建的环境有可能在这里

#### 指定虚拟环境的安装路径：从 C 盘移出

如果已有环境在 C 盘，可以手动迁移：
1. 找到原环境路径（如 `C:\Users\你的用户名\.conda\envs\myenv`）。
2. 复制整个 `myenv` 文件夹到新路径（如 `D:\conda_envs`）。
3. 更新 Conda 的索引信息：`conda config --append envs_dirs D:\conda_envs`
4. 激活环境时，Conda 会自动识别新路径。


**注意事项**
- 确保自定义路径（如 `D:\conda_envs`）有读写权限。如果提示权限不足，右键文件夹 > 属性 > 安全 > 编辑 > 添加当前用户并赋予完全控制权。
- 路径中避免使用中文或特殊字符（如空格、`!`、`#` 等），推荐纯英文路径。
- 彻底清理旧环境（可选）：
- 如果 C 盘空间不足，可以删除旧环境：
	`conda env remove --name myenv`，或直接手动删除文件夹

### 激活和退出虚拟环境

- venv： 
	在 Windows 中，使用 `myenv\Scripts\activate` 激活虚拟环境：
    在 Unix 或 MacOS 中，使用 `source myenv/bin/activate` 激活虚拟环境：
    `deactivate` 退出虚拟环境：
- Conda： 
	在 Conda 中，使用 `conda activate myenv` 激活虚拟环境：
    `conda deactivate` 退出虚拟环境：

#### 在 VS Code 中使用新路径的环境
1. 打开 VS Code，按 `Ctrl+Shift+P`，输入 `Python: Select Interpreter`。
2. 选择新路径下的 Python 解释器（如 `D:\conda_envs\myenv\python.exe`）。
3. 使用 `Ctrl+shift+'` 或导航到菜单 `view>Terminal` 打开终端
	可能出现已成功激活 Selected conda 环境，即使终端提示中可能不存在 "(minecraft)" 标记
4. 输入 `conda activate myenv` 激活需要的环境
自动激活和更改默认终端的环境可见 [在VSCode中更改专用终端的Conda环境_vscode切换conda环境-CSDN博客](https://blog.csdn.net/i89211/article/details/138900633) 
终端不显示环境的问题：[Activate Environments in Terminal Using Environment Variables · microsoft/vscode-python Wiki](https://github.com/microsoft/vscode-python/wiki/Activate-Environments-in-Terminal-Using-Environment-Variables) 

### 删除虚拟环境

```bash
conda remove --name myenv --all
```
- `--all`：删除环境中的所有包和配置。

### 虚拟环境内部管理
在虚拟环境中安装和管理依赖：
- 使用 `pip` 或 `conda` 在虚拟环境中安装所需的 Python 库，比如 `conda install numpy`
- 学会通过 `requirements.txt` 文件来管理项目的依赖。

查包命令： [conda常用命令_如何查看conda环境中安装了哪些依赖库-CSDN博客](https://blog.csdn.net/qq_35890572/article/details/132423320)

使用 conda 导入 `requirements.txt` ：
```bash
conda install --yes --file requirements.txt
```
如果 `requirements.txt` 中的某些包不可用，可以使用以下命令逐个安装包：
```bash
while read requirement; do conda install --yes $requirement; done < requirements.txt
```
如果 Conda 命令无效，可以使用 pip 作为备用：
```bash
while read requirement; do conda install --yes $requirement || pip install $requirement; done < requirements.txt
```
你也可以将环境导出为`.yml`文件，然后在其他机器上创建相同的环境：
```bash
conda env export > environment.yml
conda env create -f environment.yml
```

#### 修改 pip install 的默认位置
[修改pip 默认安装位置 - 哔哩哔哩](https://www.bilibili.com/opus/801822260725809168) 
查询当前存储信息
```bash
python -m site
```
查找目前环境的设定文件位置
```bash
python -m site help
```
使用以下命令也可以找到当前环境的配置
```bash
python -c "import site; print(site.__file__)"
```

>好像 anaconda 会直接控制包的安装位置，所以以上的似乎可以不管


## 常用指令

[Anaconda conda常用命令：从入门到精通_conda命令_笨牛慢耕的博客-CSDN博客](https://blog.csdn.net/chenxy_bwave/article/details/119996001)
安装库：`conda install ku`
列出可用环境 `conda info --envs`

| 操作       | 命令                                     |     |
| -------- | -------------------------------------- | --- |
| **创建环境** | `conda create --name myenv python=3.9` |     |
| **激活环境** | `conda activate myenv`                 |     |
| **退出环境** | `conda deactivate`                     |     |
| **删除环境** | `conda remove --name myenv --all`      |     |
