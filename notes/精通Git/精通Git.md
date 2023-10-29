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

## 变基

用于将一个分支的修改整合到另一个分支

是把某条分支线上的工作再另一个分支线上按顺序重现

### 基本的变基操作

把分支上的提交的更改以补丁的形式应用到主分支上：

git checkout [branch]

git rebase master

然后快进主分支

git checkout master

git merge [branch]

### 更有趣的变基操作

如果在分支(server)上继续创建了分支(client)

合并时，只想合并最下层的分支，又不想合并上层分支未完成的分支：

git rebase --onto master server client

意思是，切换到client分支，找出client分支与sever分支的共同祖先提交，然后把共同祖先以来client分支上单独的工作在master分支上重现

接下来，快进即可

git checkout master

git merge client

git branch -d client

### 变基操作的潜在危害

但是要注意：

不要对已经推送到远程仓库的公开提交进行变基操作

会存在同样的提交有不同的作者，日期，和提交信息，回造成困惑

### 只在需要的时候进行变基操作

如果在已经推送了提交的历史上执行变基操作，其他人可能已经在变基的基础上提交了自己的开发

这时就需要先拉取，然后重现别人的提交：

git fetch

git push --rebase

### 变基操作与合并操作的对比

没有最好，依据情况而定

最好的办法是：

对本地未推送的更改进行变基操作，从而简化提交历史

而不能对已经推送到远程仓库的更改进行变基操作

# Git服务器

## 协议

### 本地协议

此时，远程仓库是磁盘上的另一个目录

克隆本地仓库：

git clone URL.git

git clone file://URL.git

将本地仓库添加到自己的Git项目中；

git remote add [remote] URL

### HTTP协议

HTTPS成为智能HTTP，加上身份验证即可

非智能HTTP协议，不允许推送，需要设置钩子函数，开启权限

### SHH协议

非常安全，全程加密，传输效率高

不允许匿名访问

### Git协议

是Git自带的守护进程，监听9418端口

不具备任何的身份验证

但是设置很麻烦，要创建git-daemon-export-ok文件。还要配置工具

因为不安全，所以用的少

## 在服务器上搭建Git

开始配置Git服务器时候，需要把已有的仓库导出成一个新的裸仓库

即舍去工作目录，只复制出Git仓库目录

git clone --base [path-name] [url]

#### 将裸仓库放置在服务器上

将裸仓库复制到服务器目录上:

scp -r [my_bare_git] [server]

这样，其他用户就可以克隆你的仓库了

初始化时，添加--shared参数，就会被赋予写权限

git init --bare --shared

### 小型团队配置

一种是为每个团队成员行间服务器账号

一种是只在服务器上创建单个git用户，然后把需要写权限的用户把SSH公钥放置到git用户的~/.ssh/authorized_keys文件中

## 生成个人的SSH公钥

电脑上在.ssh文件下会有.pub文件（公钥）贺id_rsa/id_dss（密钥）文件

将公钥内容放到服务器即可

### # 分布式Git

## 分布式工作流

### 集中式工作流

多个开发人员共享一个代码

每次提交前，需要获取并合并最新数据，然后才能推送到仓库

### 集成管理者工作流

项目维护人员推送到公开仓库

贡献者克隆改仓库，做出自己的修改

贡献者推送到自己的公开仓库副本

贡献者香维护人员发电子邮件，要求合并变更

维护人员将贡献者的仓库添加为远程仓库并在本地合并

维护人员将合并后的变更推送到主仓库

### 司令官与副官工作流

普通开发人员使用自己的主题分支，根据master(司令官)分支进行变基

副官将开发人员的肢体分支合并入master分支

司令官将副官master分支合并入自己的master分支

司令官将其master分支推送到参考仓库，同时其他开发人员以此未基础进行变基

## 为项目做贡献

### 提交准则

检测是否存在空字符：

git diff --check

每次提交尽可能是独立的集合，每次提交只做一件事

提交消息：

> 第一行：简要的变更汇总信息（50个字符之内)
>
> 空行
>
> 第三行：详细的说明，每行72个字符内。这个第一行是主题，下面是正文，两者之间由空行隔开
>
> 空行之下是描述性信息
>
> 使用连字符或者星号作为条目符号，前面加上一个空格

### 私有小型团队

几个开发人人员共享：

推送前获取数据，然后回到master分支合并其他分支，最后推送

### 私有管理团队

