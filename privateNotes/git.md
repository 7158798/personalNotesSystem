[TOC]
## 创建版本库
创建一个版本库非常简单，
首先，选择一个合适的地方，创建一个空目录：
```
$ mkdir learngit
$ cd learngit
$ pwd
/Users/michael/learngit
```
第二步，通过git init命令把这个目录变成Git可以管理的仓库：
```
$ git init
Initialized empty Git repository in /Users/michael/learngit/.git/
```
瞬间Git就把仓库建好了，而且告诉你是一个空的仓库（empty Git repository），细心的读者可以发现当前目录下多了一个.git的目录，这个目录是Git来跟踪管理版本库的，没事千万不要手动修改这个目录里面的文件，不然改乱了，就把Git仓库给破坏了。
如果你没有看到.git目录，那是因为这个目录默认是隐藏的，用ls -ah命令就可以看见。

##时光机穿梭
运行`git status`命令看看结果：
要随时掌握工作区的状态，使用git status命令。
如果git status告诉你有文件被修改过，用git diff可以查看修改内容。
### 版本回退
HEAD指向的版本就是当前版本，因此，Git允许我们在版本的历史之间穿梭，使用命令git reset --hard commit_id。
穿梭前，用git log可以查看提交历史，以便确定要回退到哪个版本。
要重返未来，用git reflog查看命令历史，以便确定要回到未来的哪个版本。
### 工作区 暂存区
![](http://www.liaoxuefeng.com/files/attachments/001384907702917346729e9afbf4127b6dfbae9207af016000/0)
### 撤销修改
Git会告诉你，`git checkout -- file`可以丢弃工作区的修改：
Git同样告诉我们，用命令`git reset HEAD file`可以把暂存区的修改撤销掉（unstage），重新放回工作区：


## Git Bash命令行中文乱码解决方案
乱码情景一：
使用 git log 时出现乱码，执行以下命令：
```
git config --global gui.encoding utf-8
git config --global i18n.commitencoding utf-8
git config --global svn.pathnameencoding utf-8
```
乱码情景二：
使用 git status 时出现乱码，执行以下命令：
git config --global core.quotepath false



在我把网上关于修改gitconfig等文件的操作撤销后
再把gitbash设置如下
![](.\privateNotesPictures\gitbash.PNG)
再$git config --global core.quotepath false
就都正常了

此外
在windows下可以使用tortoise git这个可视化工具比较方便，这样就不会出现bash下的乱码问题了。
