---
title: Git常用命令
date: 2018-03-20 10:34:56
tags:
---
# Git常用命令
## 新建代码库
```
//在当前目录初始化为Git代码库
git init 

//新建一个目录并初始化Git代码库
git init [project-name]

//下载一个仓库/项目
git clone [url]
```

## 增加/删除文件
```
//添加文件到暂存区
git add [file] [file2]...

//添加目录到暂存区，包括子目录
git add [directory]

//添加所有文件到暂存区
git add .

//删除工作区文件，并将这次删除存入暂存区
git rm [file][file2]...

//停止追踪指定文件，但文件会保存在工作区
git rm --cached [file]

//改文件名，并将修改放入暂存区
git mv [file-original] [file-renamed]
```

## 代码提交
```
//提交暂存区到仓库区
git commit -m [message]

//提交暂存区的指定文件到仓库区
git commit [file] [file2]... -m [message]

//提交工作区自上次commit之后的变化，直接到仓库区
git commit -a

//提交时显示所有的diff信息
git commit -v

//使用新的commit，替代上一次的提交
git commit --amend -m [message]

//重做上一次的commit,并包括指定文件的新变化
git commit --amend [file] [file2]...
```

## 分支
```
//列出所有本地分支
git branch

//列出所有远程分支
git branch -r

//列出所有分支
git branch -a

//新建一个分支，但依然保留在当前分支
git branch [branch-name]

//新建一个分支，并切换到该分支
git checkout -b [branch-name]

//新建一个分支，指向指定commit
git branch [branch-name] [commit]

//新建一个分支，与指定的远程分支建立追踪关系
git branch --track [branch-name] [remote-branch]

//切换到指定分支，并更新工作区
git checkout [branch-name]

//切换到上一个分支
git checkout -

//在现有的分支和指定的远程分支建立追踪关系
git branch --set-upstream [branch] [remote-branch]

//合并指定分支到当前分支
git merge [branch]

//选择一个commit，合并进当前分支
git cherry-pick [commit]

//删除分支
git branch -d [branch-name]

//删除远程分支
git push origin --delete [branch-name]
git branch -dr [remote/branch]
```

## 查看信息
```
//显示有变更的文件
git status

//显示当前分支的版本历史
git log

//显示commit历史，以及每次commit发生变更的文件
git commit --stat

//搜索提交历史，根据关键词
git log -S [keyword]

//显示某个commit之后的所有变动，每个commit占一行
git log [tag] HEAD --pretty-format:%s

//显示某个commit之后的所有变动，其“提交说明”必须符合搜索条件
git log [tag] HEAD --grep feature

//显示某个文件的历史版本，包括文件改名
git log --follow [file]
git whatchanged [file]

//显示指定文件相关的每一次diff
git log -p [file]

//显示过去5次提交
git log 5 --pretty --online

//显示所有提交过的用户，按提交次数排序
git shortlog -sn

//显示指定文件是什么人在什么时间修改过的
git blame [file]

//显示暂存区和工作区的差异
git diff

//显示暂存区和上一个commit的差异
git diff --cached [file]

//显示工作区与当前分支最新commit之间的差异
git diff HEAD

//显示两次提交之间的差异
git diff [first-banch]...[second-banch]

//显示你今天写了多少行代码
git diff --shortstat "@ {0 day ago}"

//显示某次提交的元数据和内容变化
git show [commit]

//显示某次提交发生变化的文件
git show --name-only [commit]

//显示某次提交时，某个文件的内容
git show [commit]:[filename]

//显示当前分支的最近几次提交
git reflog
```

## 远程同步
```
//下载远程仓库的所有变动
git fetch [remote]

//显示所有远程仓库
git remote -v

//显示某个远程仓库的信息
git remote show [remote]

//增加一个新的远程仓库并命名
git remote add [shortname] [url]

//取回远程仓库的变化，并与本地分支合并
git pull [remote] [branch]

//上传本地分支到远程仓库
git push [remote] [branch]

//强行推送当前分支到远程仓库，即使有冲突
git push [remote] --force

//推送所有分支到远程仓库
git push [remote] --all 
```

## 撤销
```
//恢复暂存区的指定文件到工作区
git checkout [file]

//恢复某个commit的指定文件到工作区和暂存区
git checkout [commit] [file]

//恢复暂存区的所有文件到工作区
git checkout .

//重置暂存区的指定文件和上一次的commit保持一致，但工作区保持不变
git reset [file]

//重置暂存区和工作区，与上一次的commi保持一致
git reset --hard

//重置当前分支的指针为指定的commit，并同时重置暂存区，工作区保持不变
git reset [commit]

//重置当前分支的HEAD为指定的commit，同时重置暂存区和工作区，与指定的commit一致
git reset --hard [commit]

//重置当前HEAD为指定commit，但保持暂存区和工作区不变
git reset --keep [commit]

//新建一个commit，用来撤销并替代指定commit，并应用到当前分支
git revert [commit]

//暂时将未提交的变化移除，稍后再移入
git stash 
git stash pop
```
