# Git的首次配置

## 配置用户身份

git config --global user.name "cswuhan"

git config --global user.email "2465451104@qq.com"

### 配置个人编辑器

git config --global core.editor "'D:\Program Files\notepad++\notepad++.exe' multiInst"

### 检查个人设置

git config --list

# Git基础

## 获取Git仓库

### 现有目录中初始化仓库

git init

git add --all //跟踪文件

git commit -m "message"

### 克隆现有仓库

git clone url 

可以同时更换为想要的目录名字:

git clone myDiretory

有三种方法：

https://

ssh

git://

## 仓库中记录变更

修改被追踪的文件后，要添加到暂存区，然后提交

刚clone的文件，默认追踪所有文件

当添加文件后，会出现"untracked file",即未跟踪文件

### 查看状态

git status

### 跟踪文件

跟踪新文件，并且放到暂存区等待提交，可以理解为“添加内容到下一次提交”

git add file

### 显示更加简洁的状态信息

git status -s

git status --short

### 忽略文件

新建名为gitignore文件，用简化的正则表达式写入规则，Github官网有示例

### 查看已暂存和未暂存的变更

git diff

git diff -staged 查看哪些内容会进入下一次提交

git diff --cashed 查看当前已暂存的变更

git difftool 用工具查看

### 提交变更

git commit会打开编辑器显示

git commit -v 差异化对比

或者直接键入提交信息: git commit -m "message"

### 跳过暂存区

加入 -a

git commit -a -m "message"

### 移除文件

从暂存区中移除

git rm filename

但是想把这个文件留在磁盘中，而不想让Git对其追踪

git rm --cached filename

### 移动文件

git mv file_from file_to

## 查看提交历史

git log

git log -p 显示每次提交的差异

git log -n 显示最近的几次提交

git log --stat 简要统计

git log --pretty=oneline 单行显示提交

git log --pretty=format:"%h - %an, %ar %ae %ad | %cn %ce %cd : %s"  格式显示提交

an 作者名字，ar创建时间,ae 作者邮箱

cn 提交者名字， ce 提交者邮箱, cd 提交日期, s 提交的主题

git log --pertty=format"%h %s" --graph 显示分支和合并历史

限制提交的历史范围：

git log --since=2.week 限制两周内提交

git log --author 指定作者 --before 日期之前

## 撤销操作

如果在一次提交中遗漏了内容，可以尝试，将暂存区的内容重新提交:

git commit --amend

### 撤销已存储的文件

如果对文件的两次修改，想分两次提交，但是缺不小心把所有文件都加入了存储区

git reset HEAD filename

将不想加入存储区的文件移除

### 撤销对文件的修改

git checkout filename

## 远程仓库的使用

### 显示远程仓库

git remote 

gir remote -v 显示地址

### 添加远程仓库

git remote add [shortname] url

### 从远程仓库获取和拉取数据

git fetch [remote-name] 获取本地中没有的数据，但不会自动合并

git pull  自动拉取数据并自动合并

### 将数据推送到远程仓库

git push [remoye-name] [branch-name]

如果在推送前有其他人推送了数据，需要先拉取别人的变更，整合到自己的目录中，才能进行推送

### 检查远程仓库

查看远程仓库的更多信息

git remote show [remote-name]

### 删除和重命名远程仓库

重命名：

git remote renama original_name updated_name

删除：

git remote rm [remote-name]

## 标记

标记为特定版本

### 列举标签

git tag

### 创建标签

分为轻量标签和注释标签

轻量标签-指向某次提交的指针

注释标签-作为完成的对象存储再Git数据库中，包含详细的信息

### 注释标签

创建注释标签:

git tag -a [version] -m "mSessage"

显示标签：

git show [version]

### 轻量标签

创建轻量标签，不需要任何参数：

git tag [version]

### 补加标签

在提交完成后还可补上标签：

git tag -a [version] [提交的校验和]

### 共享标签

默认下，本地标签不会上传到远程服务器

主动推送：
git push [repo-name] [tagname]

一次性推送:

git push [repo-name] --tags

### 检出标签

在特定标签上创建分支：

git checkout -b [branch-name] [tag-name]

## Git别名

git config --global alias.[your-command-name]  [original-name]

例如，将git commit取别名

git config --global alias.ci commit

# Git分支机制

## Git分支简述

### 创建新分支

git branch [branch-name]

git branch first-table

查看各分支指向的对象

git log --oneline --decorate

### 切换分支

git checkout [branch-name]

git checkout main

HEAD指针会指向当前处于的分支

当发生提交后，当前的提交快照会向前推进，并会指向上一次提交快照（父提交）

查看分支历史

git log --oneline --decorate --graph --all

## 基本的分支与合并操作

在项目中遇到了新的问题，可以创建新分支用于解决当前的问题，解决完后，合并分支，并回到初始分支

### 基本的分支操作

当遇到新问题新任务时，新建分支并切换到这个分支上

git checkout -b [new_branch-name]

等效于：

git branch [new_branch-name]

git checkout [new_branch-name]

当前问题解决完之后，回到主分支，合并这个解决问题的分支，并删除这个分支：

git checkout master

git merge [new_branch-name]

git branch -d [new_branch-name]

### 基本的合并操作

当某个分支的工作已完成，就可以回到主分支，完成合并

当两个要合并的分支不具有直接的祖先时候，会以最近的共同祖先为基础来进行合并，并产生“合并提交”

git checkout master

git merge iss_branch

git branch -d iss_branch

### 基本的合并冲突处理

如果多个分支对同一文件进行了处理，在合并时就会产生冲突。

此时可以通过

git status

来查看冲突源，并尝试修改存在冲突的文件

或者使用图形化工具:

git mergetool来处理

## 分支管理

查看已被并入当前分支的所有分支

git branch --mergerd

如果发现分支已被并入，可将其删除：

git branch -d [branch-name]

查看未被并入当前分支的所有分支

git branch --no-merged

## 与分支有关的工作流

### 长期分支

比如master用于存放稳定版本的代码

另一个交develop或next的平行分支用于开发，这种分支还用于合并解决较小问题的分支

当小问题解决后，会合并到更高级别的分支，这个过程会一直向上递归到开发出了经过测试的稳定版本

### 主题分支

用于解决某个特定问题的主题-分支

比如，开发一个前端页面，我有三个方案，分别建立了三个分支，但是最后敲定了最好的分支，但是觉得最后一个也可以借鉴

于是我把这两个分支并入主分支

## 远程分支

远程分支是指向远程仓库的分支的指针

[remote]/[branch]远程仓库名/分支名

只要不与远程服务器通信，这个远程分支就不会改变

如果有其他人对远程仓库进行了更改，就要git fetch [remote] 获取本地数据库所没有的数据

### 推送

与别人共享这个分支的成果时。可将本地分支推送到服务器上

git push [remote] [branch]

git push cswuhan master

等价于：

git push cswuhan master:master

即把本地的分支推送到服务器上的master

还可以更改名字

git push cswuhan master:main

别人向获取你的服务器上拉取更新时，就可以：

git fetch cswuhan

此时，他有一个指向你的分支的指针，但是并没有你的指针的内容

可以把你的分支合并到他本地分支：

git checkout -b other cswuhan/master

### 跟踪分支

在跟踪分支上，可以简化命令：

git push

git pull

还可以更改当前分支所追踪的分支：

git checkout --track [remote]/[branch]

git branch -u [remote]/[branch]

如果切换的分支未被创建，且与远程服务器端的分支同名，可以直接创建，会默认为你追踪：

git checkout [branch]

查看跟踪了哪些分支：

git branch -vv

## 拉取

git fetch

git merge

先拉取，会让你选择合并

但是git pull会自动更新本地服务器

git fetch + git merge === git pull

### 删除远程分支

git push [remote] --delete [master]

删除远程服务器的分支



