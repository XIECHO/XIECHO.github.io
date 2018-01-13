---
title: git的使用
tags: [git]
categories: tools
---

# 配置用户名和Email
$ git config --global user.name "Your Name"
$ git config --global user.email "email@example.com"

# 创建版本库
初始化一个Git仓库，使用**git init**命令。
添加文件到Git仓库，分两步：
- 第一步，使用命令**git add <file>**，注意，可反复多次使用，添加多个文件；
- 第二步，使用命令**git commit -m ""**，完成。

# vim的使用
**i** 进入输入模式
**ESC** 退出输入模式，进入命令模式
**:wq** 保存修改并退出vim

<!--more-->

# 状态的查看和比较
- 比较 git diff
- 查看 git status 文件名

# 版本回退
- 查看历史 git log/git log --pretty=online
当前版本用HEAD表示，HEAD^表示上一个版本，HEAD^^表示上上版本，HEAD~100表示上100个版本
- 回退到当前版本的上一个版本 git reset --hard HEAD^
当你回退到以前版本，那当前版本会不见，可以使用 git reset --hard (commit id)来恢复
- 记录执行的每一次命令 git reflog
通过此条命令可以查看到各个版本commit id

HEAD指向当前版本
git log 查看提交历史
git reflog 查看命令历史

# 工作区和暂存区
- 工作区(Working Directory)
就是当前目录
- 版本库(Repository)
工作区中隐藏目录.git,Git的版本库
版本库中有：暂存区、第一个分支master、指向master的一个指针HEAD
- 暂存区(Stage)
**把文件往Git版本库里添加的时候，分为两步**
第一步：git add，意义是把文件添加到暂存区
第二步: git commit,意义是将暂存区的所有内容提交到当前分支
开始默认我们在master分支

Git是如何跟踪修改的：每次修改，如果不add到暂存区，那就不会加入到commit中。

# 撤销和修改
命令是：**git checkout -- filename**
- file自修改后还没有被放到暂存区，使用命令后，返回版本库的状态
- file已经添加到了暂存区，又作了修改，使用命令后，返回暂存区的状态
总之，是文件返回最近一次git commit 或 git add 的状态

命令：git reset HEAD file
指的是把暂存区的修改撤销，回到工作区的版本
git reset 既可以回退版本，也可以把暂存区的修改回退到工作区。

总结：
- 场景1：当你改乱了工作区某个文件的内容，想直接丢弃工作区的修改时，用命令git checkout -- file。
- 场景2：当你不但改乱了工作区某个文件的内容，还添加到了暂存区时，想丢弃修改，分两步，第一步用命令git reset HEAD file，就回到了场景1，第二步按场景1操作。
- 场景3：已经提交了不合适的修改到版本库时，想要撤销本次提交，参考版本回退一节，不过前提是没有推送到远程库。

# 删除文件
将已经提交到版本库的文件删除，需要同步git
1. git rm file 
2. git commit -m ""
如果是误删
git checkout -- file

# 添加远程仓库
1. 要关联一个远程库，使用命令**git remote add origin git@server-name:path/repo-name.git;
2. 关联后，使用命令**git push -u origin master** 第一次推送master分支的所有内容;
3. 此后，每次本地提交后，只要有必要，就可以使用命令**git push origin master**推送最新修改;

## Tips 
ssh:是一个安全协议，git支持git协议。第一次使用ssh的时候，需要设置公钥和私钥，命令是
- ssh-keygen -t rsa -C "youremail@example.com"
对应的在用户主目录中会生成.ssh目录，目录中有id_rsa和id_rsa.pub两个文件

# clone远程库
命令是**git clone git@server-name:path/repo-name.git**
git支持多种协议，包括https，ssh 等等

# 创建与合并分支
- **git checkout -b dev**:创建了dev分支
命令等同于：git branch dev ; git checkout dev
- **git branch**:查看当前分支，罗列出所有分支
- **git merge dev**:将dev分支的工作成果合并到当前分支上
- **git branch -d dev**:删除dev分支

# 解决冲突
当Git无法自动合并分支时，就必须首先解决冲突。解决冲突后，再提交，合并完成。
用**git log --graph**命令可以看到合并图。
好看一点用git log --graph --pretty=oneline --abbrev -commit

# 分支策略
- master分支用来发布新版本，平时不东
- dev分支是用来干活的，干完活和master合并
- 每个团队成员创建自己的分支，是不是和dev分支合并

合并时，默认是fast forward合并，合并后删除分支后看不出是合并的，会丢失信息，加上--nn-ff参数就可以使用普通模式合并

# Bug分支
当我们遇到bug需要修复，手头的任务又没有做完，我们可以使用**git stash**来保护现场，类似于进程中断。当我们修复好bug后，我们可以用**git stash list**查看工作现场。
- git stash
- git stash list
- git stash apply:恢复现场，但不删除stash
- git stash drop:删除stash
- git stash pop:等于上两步

# feature分支
开发一个新feature，最好创建一个分支；如果要丢弃一个没有被合并过的分支，可以通过git branch -D name 强行删除。

# 多人协作
- git remote :用于查看远程库的信息
- git remote -v :用于查看远程库的详细信息
- git push origin master/dev :master分支需要和远程同步，dev分支也一样，bug分支不需要，feature分支看情况

