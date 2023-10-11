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



