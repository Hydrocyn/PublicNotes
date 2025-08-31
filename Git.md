---
tags:
  - Tools
---

[Git 教程 | 菜鸟教程 (runoob.com)](https://www.runoob.com/git/git-tutorial.html)
[Git - 安装 Git (git-scm.com)](https://git-scm.com/book/zh/v2/%E8%B5%B7%E6%AD%A5-%E5%AE%89%E8%A3%85-Git)
参考书：Git 版本控制管理：jon loeliger
[Learn Git Branching](https://learngitbranching.js.org/?locale=zh_CN)  交互式学习 git

## 交互问题

### bash 命令行操作

`$ mkdir ~/public_html`：在当前目录下创建名为 public_html 的子目录
	`midir` 命令用于创建新的目录
`$ cd ~/public_html` ：进行路径地址跳转
>出现错误：`bash: mkdir ~/public_html: No such file or directory`
>原因：需要使用绝对路径 `$ mkdir D:/public_html`

### 设置交互式编辑器

设置 GIT_EDITOR 环境变量以更改交互式编辑器
```
#在tcsh中
$ setenv GIT_EDTOR emacs
#在bash中
$ export GIT_EDITOR=vim
```
若要终止此次填写，只需要不保存退出编辑器即可（产生一条空日志消息）
如果已经保存了，则需要删除整条日志消息，然后重新保存。Git 不会处理空提交。

### 移动文件带来的路径问题
[Git 本地 Git 仓库移动后如何修复路径|极客教程 (geek-docs.com)](https://geek-docs.com/git/git-questions/84_git_how_do_i_fix_the_path_of_my_local_git_repo_after_move.html) 
不要随便移动程序所在位置！我通过删除重下完成了移动和程序使用的修复，太难顶了 20240925


## 工具参数

### 配置提交作者
可以用 git config 命令在配置文件里保存身份
`$ git config user.name "Jon"`
`$ git config user.emal "j@example.com"`
也可以使用 GIT_AUTHOR_NAME 和 GIT_AUTHOR_EMAIL 环境变量来填写 git 姓名和 email 地址



### 创建版本库副本
通过克隆获取项目并保持与其他版本同步
在主目录里创建一个副本：
```
$ cd d:/
$ git clone public_html my_website
```
检查两个版本库的细微差别：
```
$ ls -lsa public_html my_website
$ diff -r public_html my_website
```

### 配置文件
git 的配置文件都是简单的. ini 文件风格的文本文件
git 支持不同层次的配置文件：
`.git/config`：版本库特定的配置设置，可用--file 选项修改，是默认选项。这些配置拥有最高优先级
`~/.gitconfig`：用户特定的配置设置，可用--global 修改，windows 下是%USERPROFILE%/.config 
`/etc/gitconfig`：系统范围的配置设置。如果你有它的 UNIX 文件写权限，就可以用--system 选项修改它。这些设置的优先级最低，根据实际安装情况，这个系统设置文件可能在其他位置（如/usr/local/etc/gitconfig），也可能完全不存在

建立一个作者名和 email 地址，用于对所有版本库的所有提交，可以用 git config --global 命令给在 `$HOME/.gitconfig` 文件里的 user. name 和 user. email 赋值
```
$ git config --global user.name "Jon Loeliger"
$ git config --global user.email "jdl@example.com"
```
设置一个版本库特定的名字和 email 地址，覆盖--global 的设置，只需要省略--global 标志
```
$ git config user.name "Jon Loeliger"
$ git config usr.email "jdl@special-project.example.com"
```
使用 git config -1 列出在整组配置文件里共同查找的所有变量的设置值
因为配置文件只是简单的文本文件，所以可以通过 cat 命令来查看其内容，也可以通过文本编辑器来查看它
```linux 
# 只看版本库特定的设置
$ cat .git/config 
```
可以使用--unset 选项来移除设置
`$ git config --unset --global user.email`

### 配置别名

为经常输入的复杂命令设置一个简单的别名
`$ git config --global alias.show-graph \ 'log --graph --abbrev-commit --pretty=online'`

> [!note] 一次提交是两步过程：暂存变更和提交变更
> 在工作目录下而不在索引中的变更是没有暂存的，因此也不会提交
> 当添加或更改文件时，可以将两步合成一步
> `$ git commit index.html`
> 如果要移动或者删除文件，则两步分开
> `$ git rm index.html`
> `$ git commit`





## 文件管理
### 文件分类
Git 降所有文件分为3类：以追踪的、被忽略的以及未追踪的
可以使用 git status 获得文件状态
已追踪的（Tracked）：已追踪的文件是指已经在版本库中的文件，或者是已暂存到索引中的文件。如果想将新文件 somefile 添加为已追踪的文件，执行 git add somefile
被忽略的（Ignored）：被忽略的文件必须在版本库中被明确声明为不可见或被忽略，即使他可能会在你的工作目录中出现。普通被忽略的文件包括临时文件、个人笔记、编译器输出文件以及构建过程中自动生成的大多数文件等。
未追踪的（Untracked）：为追踪的文件是指那些不在前两类中的文件。


### git add 的使用
git add 将一个未跟踪的文件转化为已跟踪的文件。如果作用于一个目录名，则该目录下的文件和子目录都会递归暂存起来

git 在发出 git add 命令时每个文件的全部内容都将被复制到对象库中，并且按文件的 SHA 1 名来索引。暂存一个文件也称作缓存（caching）一个文件，或“将文件放入索引”

使用 `git ls-files` 查看隐藏在对象模型下的东西，并且可以找到暂存文件的 SHA 1 值（使用 `$ git ls-file --stage`）
在仍和编辑后，提交变更前须执行 git add 命令，以更新索引。否则会得到两个不同版本的文件：一个在对想哭中被捕获且索引引用，另一个在工作目录下

散列值和索引将 git add 看作“添加文件内容”而不是“添加文件”
- 须记住工作目录下的文件版本和索引中暂存的文件版本可能是不同步的

对于 git add 或 git commit 而言，--interactive 选项都会是探索哪个文件将为提交而暂存的有用方式




### git rm 的使用

git rm 与 git add 相反，它在版本库和工作目录同事删除文件。删除文件必添加文件要求更多。
从工作目录和索引中删除一个文件，并不会删除该文件在版本库中的历史记录。文件的任何版本，只要是提交到版本库的历史记录的一部分，就会在对象库里并保存历史记录。

git rm 是一条对索引进行操作的命令，她对没有添加到版本库或索引中的文件是不起作用的。因此要先 git add 添加文件

要将一个文件由已暂存的转化成未暂存的，可以使用 git rm --cached 命令：`$ git rm --cached oops`，它会删除索引中的文件并把它保留工作目录中，而 git rm 则会将文件从索引和工作目录中都删除。

>[!example] 报错
> ```
> $ git rm oops
> error: the following file has changes staged in the index:
>     oops
> (use --cached to keep the file, or -f to force removal)
> ```
> 原因:
> git 在删除一个文件之前它会先检查以确保工作目录下的该文件的版本与当前分支中的最新版本是匹配的。从而方式文件的修改意外丢失。

> [!warning] 
> 使用 git rm --cached 会把文件标记位未追踪的，却在工作目录下仍留有一个副本。这会容易忘记这个文件是不再被追踪的，而 git 总是检查工作文件内容是最新的，这种方法绕过了这个检查

### git mv 的使用

如果要移动或者重命名文件，可以对旧文件使用 git rm 命令，然后用 git add 命令添加新文件，或者可以直接使用 git mv 命令。
如将 suff 文件重命名为 newstuff，以下两种操作等价
```
$ mv stuff newtusff
$ git rm stuff
$ git add mewstuff
```
和
```
$ git mv stuff newstuff
```
其工作逻辑是：git 在索引中删除 stuff 的路径名，并添加 newstuff 的路径名，至于 stuff 的原始内容，则仍保存在对象库中，然后才会将它与 newstuff 重新关联。

git 会记得全部历史记录，但是显示要限制于在命令中指定的文件名。--follow 选项会让 git 在日志中回溯并找到内容相关联的整个历史记录。
`$ git log --follow mtdata`
VCS 的经典问题之一就是文件重命名会导致他们丢失对文件历史记录的追踪，而 git 及时经历过重命名，也仍然能保留此信息。

追踪重命名是个复杂的问题，目前还没有能完美处理文件重命名的系统

## .gitinore 文件编写




git 对象库中每一个对象都有一个唯一的名称，它是向对象内容应用 SHA 1 得到的 SHA 1 散列值。SHA 1 的值是个 160 位数，通常表示为 40 位的十六进制数。SHA 1、散列码、对象 ID 指的是同一个东西，也就是全局唯一标识符。

### obsidian git 指令含义

手动模式
`Git: Open source control view`
![[ObsidianGit手动操作面板.png]]
先 backup，再 commit，之后会自动Push

## 实践记录与碎片
我突然在想，有机化合物和机理图片，能不能也用程序生成？
UP 主玄离 199 有一个简单的 git 使用教程，还有一个在安卓手机上安装 linux 系统的

## 库创建和文件端粒

### 在本地创建一个新的仓库

本地库初始化： `$ git init`
	将当前目录转化为 git 版本库。此时 git 会创建一个. git 的隐藏目录，存放修订信息

向本地库中添加需要跟踪的文件： `$ git add <name>`
	`$ git add index.html` 添加单独文件
	`$ git add .` 添加所有文件
此时运行 `git status` ，显示中间状态的 index. html 

>warning: in the working copy of 'index. html', LF will be replaced by CRLF the next time Git touches it
>这个警告信息表明Git在处理文件`index.html`时，会将文件中的换行符从LF（Linux和Mac系统使用的换行符）转换为CRLF（Windows系统使用的换行符）

进行提交：`$git commit`
	如果不通过命令行直接提供日志消息，git 会启动编辑器，并提示你写一个。
	一条完全限定的 git commit 命令必须提供日志消息和作者：
	`$ git commit -m "Initial contents of public_html" \ --author="Jon Loeliger <jdl@example.com>`
	`git commit -a` 选项会导致执行提交之前自动暂存所有未暂存的和未追踪的文件变化，包括从工作副本中删除已追踪的文件

参考：[还不会使用 GitHub ？ GitHub 教程来了！万字图文详解 - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/369486197) 

### 从远程克隆一个仓库

```bash
git clone URL
```

克隆完成后会保留. git 文件，并且绑定远程库


### 文件的移动和删除

git rm 表示你想要删除这个文件的意图并暂存这个变更，接着使用 git commit 在版本库里实现这个变更。
```linux
$ cd ~/public_html 
$ ls
$ git rm poem.html #删除文件
$ git commit -m "Remove a poem" #可以省略-m 选项，然后在文本编辑器中以交互方式输入日志消息
```


可以使用 git rm 和 git add 组合命令来间接为一个文件重命名
```linux 
$ mv foo.html bar html 
$ git rm foo.html 
$ git add bar.html 
```
必须先执行 mv foo. html bar. html，以防 git rm 命令会把 foo. html 从文件系统中永久删除

也可以更快而直接地通过 git mv 命令来做到
```linux 
$ git mv foo.html bar.html 
# 暂存地变更必须随后提交
$ git commit -m "Moved foo to bar"
```

### 提交历史与版本回滚

**检查历史记录**
`git log` 命令会产生版本库里一系列单独提交的历史
可以使用 `git show` 命令带一个提交码，查看特定提交的更加详细的信息
使用 `show-branch`，提供当前开发分支简洁的单行摘要
``$ git show-branch --more=10`，参数 `--more=10` 表示额外 10 个版本

**查看提交差异**
使用两个提交的全 ID 名并运行 `git diff`，如
`$ git diff hex1 \ hex2`，git 提供了更短、更简洁的方式来执行这样的命令，而无需产生这样大而复杂的数字
`$ git diff` 显示仍留在工作目录中且未暂存的变更；
`$ git diff —cached` 显示已经暂存并且因此要有助于下次提交的变更


### 本地修改或新增了文件


### 删除本地仓库

```bash
rm -rf .git
```

## 关联远程 github 仓库

检查远程仓库状态，显示远程仓库的 URL 和状态
```cpp
git remote -v
```

当你在执行 Git 命令时遇到错误信息 `fatal: not a git repository (or any of the parent directories): .git`，这表明你当前所在的目录不是一个 Git 仓库，或者你的工作目录不在 Git 仓库的根目录下。

关联远程仓库：
```bash
git remote add origin https://github.com/Hydrocyn/MyNoicePractice.git
```
其中 `origin` 为远程仓库的名称，作用是将此名称与远程库的 URL 相关联

### 将本地合并的修改推送到 github

如果已经合并到了 origin 并推送给 github，此时本地分支是最新的，直接使用
```bash
git push origin main  # 或者 origin/master，根据你的远程分支名称
```


## 多人协作

### 创建分支

### 远程端被其他开发者修改了文件

情形：确保本地分支是最新的/合并过程有冲突/远程端有其他人更改/处理推送错误

考虑到远程则使用如下命令拉取远程分支的最新更改
```bash
git fetch origin
git merge origin/main  # 或者 origin/master，根据你的远程分支名称
```
或者使用
```bash
git pull origin main  # 或者 origin/master
```

**`git pull`** 是 `git fetch` 和 `git merge` 的组合命令。它会自动获取远程更改并尝试合并到当前分支。
	 **`git fetch`**：从远程仓库获取最新的更改，但不会自动合并到本地分支。你需要手动合并。
	 **`git merge`**：将远程分支的更改合并到当前分支。

### 解决合并冲突 (可能)

如果在合并过程中出现冲突，你需要手动解决冲突，然后标记冲突已解决：
```bash
git add <conflicted-files>
git commit
```

### 切换分支与合并分支

github 库是 main，但本地建立了 master，如果直接推送会覆盖还是将两个分支同时存在？
	如果GitHub远程仓库的默认分支是`main`，而本地仓库的默认分支是`master`，直接推送本地的`master`分支到远程仓库不会覆盖远程的`main`分支，而是会在远程仓库中创建一个新的分支`master`。这意味着远程仓库中将同时存在`main`和`master`两个分支。
强行进行会出现如下报错：
```
There is no tracking information for the current branch.
Please specify which branch you want to merge with.
See git-pull(1) for details.

    git pull <remote> <branch>

If you wish to set tracking information for this branch you can do so with:

    git branch --set-upstream-to=origin/<branch> master

```

**强制覆盖远程分支**
如果你希望将本地的 `master` 分支推送到远程的 `main` 分支，并覆盖远程的 `main` 分支，可以使用以下命令，这会将本地 `master` 分支的内容推送到远程的 `main` 分支，并覆盖远程的 `main` 分支。
```bash
git push origin master:main --force
```

**本地迎合远程**
如果你希望将本地分支 `master` 重命名为 `main`，并将其与远程的 `main` 分支关联，可以按照以下步骤操作：
1. **重命名本地分支**
```bash
git branch -m master main
```
2. **推送到远程仓库**
将新的本地分支 `main` 推送到远程仓库，并设置远程分支的关联：
```bash
git push origin -u main
```

3. **删除远程的 `master` 分支（如果需要）**
如果你希望删除远程的 `master` 分支，可以运行以下命令：
```bash
git push origin --delete master
```

**远程迎合本地**
如果你希望将远程分支 `main` 重命名为 `master`，可以按照以下步骤操作（其实是建立一个新分支然后删除旧分支）：
1. **重命名远程分支**
在远程仓库中，重命名分支通常需要使用 Git 的 `push` 命令。例如：
```bash
git push origin main:master
```
这会将远程的 `main` 分支重命名为 `master`。
2. **删除远程的 `main` 分支**
```bash
git push origin --delete main
```
3. **更新本地分支的上游分支**
确保本地分支与新的远程分支关联：
```bash
git branch --set-upstream-to=origin/master master
```

**变基（可选）**
如果你希望将本地的更改应用到远程 `main` 分支的顶部，可以使用 `git rebase`：
```bash
git rebase origin/main
```
如果在变基过程中出现冲突，解决冲突后继续变基：
```bash
git rebase --continue
```

### 跟踪上游分支
可以让本地 `master` 分支知道它应该跟踪远程的 `main` 分支。可以使用以下命令：
```bash
git branch --set-upstream-to=origin/main master
```

### 本地有内容，远程有仓库的矛盾
方法：把本地的文件建立一个副本，`git clone` 拉取远程库，然后将本地内容恢复，再推送到远程
 [Git -- 如何删除本地仓库_怎么删除本地仓库-CSDN博客](https://blog.csdn.net/bloombud/article/details/80431557) 

> `git clone` 会在 git 当前目录生成远程库名的文件夹（`Laboratory` 下使用 `https://github.com/Hydrocyn/MyNoicePractice` ，则会生成 `Laboratory\MyNoicePractice`），所以要在上级目录中安放才能保证位置

### 库结构的调整
在 deepseek 中已有讨论，这有关 file-repo 的使用和强制推送

如何移动带有 git 的文件夹？如果进行移动，如何同步 github 进行管理？

```bash
Laboratory/                 
├── .git/                    
├── code/
	└── cpractice/      
├── Revolution/                      
├── simulation/ 
├── README/ 
└── .gitinore
```

### git clone 拉取库和分支




### 项目的迁移和自动化部署

#### 使用 Git 子模块管理/版本库嵌套

如果在一个版本库中添加另一个版本库，则会出现
```
hint: You've added another git repository inside your current repository.
hint: Clones of the outer repository will not contain the contents of
hint: the embedded repository and will not know how to obtain it.
hint: If you meant to add a submodule, use:
hint:
hint:   git submodule add <url> tmp/commit-all-example
hint:
hint: If you added this path by mistake, you can remove it from the
hint: index with:
hint:
hint:   git rm --cached tmp/commit-all-example
hint:
hint: See "git help submodule" for more information.
```


#### 编写脚本自动化下载和编译库
比如
```bash
#!/bin/bash

# 下载第三方库
git clone https://github.com/user/third-party-lib.git third-party-lib

# 编译第三方库
cd third-party-lib
./configure
make
make install
cd ..

# 将库的路径添加到环境变量中（如果需要）
export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/path/to/third-party-lib/lib
```

注意修改本地分支的问题

### 分支管理

使用 `git branch` 查看当前仓库分支
使用 `git branch -a` 查看所有分支

### 删除远程仓库



## 远程版本库与同步

交换文件用的版本库称为远程版本库 remote resposity，此版本库不一定是物理上远程的，也可能只是存在放本地文件系统中的另一个版本库

关联远程版本库操作： [[Github#本地有 Git 仓库]]

使用 git remote 命令创建、删除、操作和查看远程版本库。引入的所有远程版本库都记录在 `.git/config` 文件中，可以用 git config 来查看（但不好用）

除了 `git clone` 之外，跟远程版本库有关的其他常见的 git 命令有：
`git fetch`：从远程本本库抓取对象及其相关的元数据
`git pull`：跟 `git fetch` 类似，但合并修改到相应的本地分支
`git push`：转移对象及其相关的元数据到远程版本库
`git ls-remote`：显示一个给定的远程版本库（在上游服务器上）的引用列表

详细的 [git remote 命令 | 菜鸟教程](https://www.runoob.com/git/git-remote.html) 说明和使用
	`git remote add origin <REMOTE_URL>`，将名称 `origin` 与 `REMOTE_URL` 相关联。
	`git remote set-url`
	`git remote -v` 显示远程库和对应的克隆地址

[关于远程仓库 - GitHub 文档](https://docs.github.com/zh/get-started/getting-started-with-git/about-remote-repositories) 
[管理远程仓库 - GitHub 文档](https://docs.github.com/zh/get-started/getting-started-with-git/managing-remote-repositories)

>[!example] git push 报错
> [git push报错：The current branch master has no upstream branch-阿里云开发者社区 (aliyun.com)](https://developer.aliyun.com/article/764975)
> 原因: 没有将本地的分支与远程仓库的分支进行关联
> [git - fatal: The current branch master has no upstream branch - Stack Overflow](https://stackoverflow.com/questions/23401652/fatal-the-current-branch-master-has-no-upstream-branch)


很多文件的管理是有方法的
![[Pasted image 20250329224601.png]]

只要将想要忽略的文件的文件名加到同一目录下的 `.gitignore` 文本文件即可忽略任何文件
`.gitignore` 文件下可以包含一个文件名模式列表，指定哪些文件要忽略。
`.gitignore` 文件的格式如下
- 空行会被忽略，而以 `#` 开头的行可以用于注释（不能用在文本后面）
- 一个简单的字面置文件名匹配任何目录中的同名文件
- 目录名由末尾的反斜线 `/` 标记，这能匹配同名的目录和子目录，但不匹配文件或符号链接。
- 包含 shell 通配符，如 `*`, 这种模式可拓展为 shell 通配模式。一个型号只能匹配一个文件或目录名。但对于一些通过斜线来指定目录名的模式（eg, `debug/32bit/*.o`），星号仍可以称为其中一部分
- 起始的感叹号 `!` 会对改行其余部分的模式进行取反。此外，被之前模式排除但被取反规则匹配的文件是要包含的。取反模式会覆盖低优先级的规则。

git 允许在版本库中任何目录下有 `.gitignore` 文件，每个文件都只影响该目录及其所有子目录。`.gitignore` 的规则也是级联的：可以覆盖高层目录中的规则，只要在其子目录包含一个取反模式（使用起始的 `!`）

使用指令 `$ echo main.o > .gitignore`，可以将文件 main. o 添加到. gitignore 中去，后者不需要提前创建

带多个 `.gitignore` 目录的层次结构问题/允许命令行对忽略文件列表的增编，git 按照下列从高到低的优先顺序：
- 在命令行上指定的模式
- 从相同目录的 `.gitignore` 文件中读取的模式
- 上层目录中的模式，向上进行。当前目录的不是能推翻上层目录的模式，而最接近当前目录的上层目录的模式优先于更上层的目录的模式（我没看懂，真的）
- 来自 `.git/info/exclude` 文件的模式
- 来自配置变量 `core.excludefile` 指定的文件中的模式

`.gitignore` 被视为普通的文本文件，在复制过程中会被复制并适用于版本库的所有副本
如果排除模式某种程度上特定于你的版本库，并且不应该（或可能不）适用于其他人复制的版本库，那么这个模式应该放到 `.git/info/exclude` 文件里，因为它在复制操作期间不会传播。它的模式的格式和适用对象与 `.gitignore` 文件是一样的。

>[!exam] 排除 `.o` 文件，需将 `*.o` 添加到顶层的 `.gitignore` 文件中
> 如果要追踪一个不是本人生成的特定的 `*.o` 文件，可以进行如下配置
> ```
> $ cd my_package 
> $ cat .gitignore 
> *. o
> $ cd my_package/vendor_files 
> $ cat .gitignore 
> !driver. o
> ```
> 这意味着 git 会忽略版本库中所有的. o 文件，但是会追踪一个例外，即在 vendor_files 子目录下的 driver. o 文件


## substree 子库

同步子库专用
`git subtree push --prefix=PublicNotes publicnote master`