title: git常用命令
author: Tutu
tags:
  - Git
categories:
  - Git
date: 2019-10-14 14:54:00
---
Git 是一个开源的分布式版本控制系统，用于敏捷高效地处理任何或小或大的项目。
Git 是 Linus Torvalds 为了帮助管理 Linux 内核开发而开发的一个开放源码的版本控制软件。
Git 与常用的版本控制工具 CVS, Subversion 等不同，它采用了分布式版本库的方式，不必服务器端软件支持
Git 不仅仅是个版本控制系统，它也是个内容管理系统(CMS)，工作管理系统等。
git学习常用命令

   | 命令 | 作用 |
   | -- | -- |
   |mkdir：| XX (创建一个空目录 XX指目录名)|
   |pwd：   |       显示当前目录的路径。|
   |git init |把当前的目录变成可以管理的git仓库，生成隐藏.git文件。|
   |git add XX  | 把xx文件添加到暂存区去。
   |git commit –m "xx" | 提交文件 –m 后面的是注释。
   |git status   | 查看仓库状态
   |git diff  XX | 查看XX文件修改了那些内容
   |git log      | 查看历史记录 9ba77981e50d3df1d71e760dd43c049d79a44b6d
   |git reset  --hard HEAD^ 或者 git reset  --hard HEAD~ | 回退到上一个版 本(如果想回退到100个版本，使用git reset --hard HEAD~100 )
   |git  reflog    | 查看历史记录的版本号id
   |git  reset --hard | 版本号  (回到某个版本)
   |cat XX        |  查看XX文件内容
   |git checkout — XX |  把XX文件在工作区的修改全部撤销。
   |git rm XX         | 删除XX文件
   |git remote add origin https://github.com/tugenhua0707/testgit | 关联一个远程库
   |git remote remove origin  | 删除remote
   |git push –u(第一次要用-u 以后不需要) origin master | 把当前master分支推送到远程库
   |git clone https://github.com/tugenhua0707/testgit  | 从远程库中克隆
   |git checkout –b dev | 创建dev分支 并切换到dev分支上  //拉取远程分支
   |git branch  | 查看当前所有的分支
   |git checkout master | 切换回master分支
   |git merge dev    | 在当前的分支上合并dev分支
   |git branch –d dev | 删除(本地的)dev分支
   |git push origin :dev | (同步删除线上的分支)
   |git branch name  | 创建分支(本地创建分支)
   |git push origin probranch(本地):probranch | (上传到线的分支)
   |git stash | 把当前的工作隐藏起来 等以后恢复现场后继续工作
   |git stash list | 查看所有被隐藏的文件列表
   |git stash apply | 恢复被隐藏的文件，但是内容不删除
   |git stash drop | 删除文件
   |git stash pop | 恢复文件的同时 也删除文件
   |git remote | 查看远程库的信息|
   |git remote –v | 查看远程库的详细信息|
   |git push origin master  | Git会把master分支推送到远程库对应的远程分支上
   |git checkout -b 本地分支名 origin/远程分支名 | 将远程git仓库里的指定分支拉取到本地（本地不存在的分支）
   |git push --set-upstream origin 分支名 | git push --set-upstream origin 分支名
   |git config --global credential.helper store | 免密码命令 输入命令后再次输入账号密码 以后都可以不用输入密码了|
   |git fetch --prune|远端有新增分支，git fetch可以同步到新的分支到本地，但是远端有删除分支，直接"git fetch"是不能将远程已经不存在的branch等在本地删除的|
   |git reset --hard origin/master|你想让本地直接和远程保持同步，想让不再提示这个讨厌信息，那么如果你本地的commit确保不想要|
  |git branch -u origin/master | 或者还有一个将本地代码与服务器代码更新一致的语句|
  |git push -f origin master| 如果想直接回退版本让远程和本地代码保持一致，那就确保本地代码没问题之后强制推到远程|
  |git log --author="tuwei" dormRoom --since="2019-10-17 00:00:00"  --pretty=tformat: --numstat | awk '{ add += $1; subs += $2; loc += $1 - $2 } END { printf "added lines: %s, removed lines: %s, total lines: %s\n", add, subs, loc }'| 统计上传代码及修改代码行数|
