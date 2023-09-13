---
title: Git之提交代码
date: 2021-02-22 12:57:37
summary: 你不能只问顾客要什么，然后想法子给他们做什么。等你做出来，他们已经另有新欢了。
categories: Git
tags: 
	- Git
---

###　Typora使用小tips：

指令前加$是只针对Linux的指令。

### 指令：首次

```bash
cd existing_folder                        # cd到项目的目录
git init                                  # 初始化本地仓库
git remote add origin giturl　            # 本地添加远程，giturl是ssh形式
git add .　                               # 将本目录下所有文件加到索引区
git commit　                              # 将索引区数据加到历史区
git push -u origin master　               #上传master分支 。//如果这里提示没有权限，是因为你的ssh配置有问题，需要重新配置
```

### 指令：修改后以后每次提交：-u是针对Gitlab

```bash
git add .			   # 全部添加。
git commit -u '做了一次修改'     # ''里面的内容是自定义的，可以为你每次修订的内容，但不能重复。
git push                # 用git push更新
```

### 指令：修改后以后每次提交：-m是针对Github

```bash
git add .			   # 全部添加。
git commit -m '做了一次修改'     # ''里面的内容是自定义的，可以为你每次修订的内容，但不能重复。
git push                # 用git push更新
```

> 注意：
>
> ```bash
>  #github首次提交代码
>  git push --set-upstream origin login
> ```
>
> 

###　创建+切换分支：

创建分支的同时切换到该分支上，命令如下：

```bash
git checkout -b [branch name]
```

git checkout -b [branch name] 的效果相当于以下两步操作：

```bash
git branch [branch name]
git checkout [branch name]
```

查看文件状态：

```bash
git status
```

提交所有代码

```bash
git add .
```

再次查看状态：

```bash
git status
```

此时本地有一个新分支，但没有同步到远程，用以下指令同步，第一次的指令如下(假如新建立的分支为user)：

```bash
# origin为云端仓库的别名，云端仓库用user分支保存
git push -u origin user
```

以后更新只需要用以下指令即可：

```bash
git push
```

### 合并分支打主分支：master

更新本地的master代码，示例：将user代码合并到主分支main分支

```bash
git merge user
```

推送到远程：

```bash
git push
```

### 切换到远程分支

[博客链接](https://blog.csdn.net/astonishqft/article/details/83029490)

查看远程所有分支

```bash
$ git branch -a
```


git branch不带参数,列出本地已经存在的分支，并且在当前分支的前面用*标记，加上-a参数可以查看所有分支列表，包括本地和远程，远程分支一般会用红色字体标记出来

* dev
 master
 remotes/origin/HEAD -> origin/master
 remotes/origin/master
 remotes/origin/release/caigou_v1.0

* 新建分支并切换到指定分支

* ```bash
 git checkout -b dev origin/release/caigou_v1.0
git checkout -b 本地分支名 origin/远程分支名
 ```
 ```

该命令可以将远程git仓库里的指定分支拉取到本地，这样就在本地新建了一个dev分支，并和指定的远程分支release/caigou_v1.0关联了起来。

Switched to a new branch 'dev'
Branch 'dev' set up to track remote branch 'release/caigou_v1.0' from 'origin'
原文链接：https://blog.csdn.net/astonishqft/article/details/83029490


 ```

### Git创建文件:使用git bash

```bash
touch README.md
git add README.md
```

