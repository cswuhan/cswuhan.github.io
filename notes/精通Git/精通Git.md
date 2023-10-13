## 配置用户身份

git config --global user.name "cswuhan"

git config --global user.email "2465451104@qq.com"

## 配置个人编辑器

git config --global core.editor "'D:\Program Files\notepad++\notepad++.exe' multiInst"

## 检查个人设置

git config --list

## 现有目录中初始化仓库

git init

git add --all //跟踪文件

git commit -m "message"

## 克隆现有仓库

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

查看状态：

git status

跟踪新文件，并且放到暂存区等待提交，可以理解为“添加内容到下一次提交”

git add file



## 显示更加简洁的状态信息

git status -s

git status --short

## 忽略文件

新建名为gitignore文件，用简化的正则表达式写入规则，Github官网有示例

## 查看已暂存和未暂存的变更

git diff

git diff -staged 查看哪些内容会进入下一次提交

git diff --cashed 查看当前已暂存的变更

git difftool 用工具查看

## 提交变更

git commit会打开编辑器显示

git commit -v 差异化对比

或者直接键入提交信息: git commit -m "message"

## 跳过暂存区

加入 -a

git commit -a -m "message"

## 移除文件

从暂存区中移除

git rm filename

但是想把这个文件留在磁盘中，而不想让Git对其追踪

git rm --cached filename

## 移动文件

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







