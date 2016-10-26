---
layout:     post
title:      "Git:时光机"
subtitle:   "Git-Time-Machine"
date:       2016-10-13 11:20:15
author:     "Gcelaor"
header-img: "img/Git.jpg"
catalog: true
tags:
    - Git
    - Github
    
---

## 提交记录

**场景**：希望查看仓库的中所有提交的信息，比如提交人、提交时间、代码增删、Commit ID等。

**步骤**：通过`git status`和`git log`可查询这些信息。

```
# 查看Git提交的元信息
git log
# 查看Git提交，以及对应的代码增删
git log -p
# 查看app.js的Git提交日志
git log -p app.js

```

## Git Blame

**场景**：查看每一行代码的最后改动时间，以及提交人。例如，追溯`app.js`文件中某一行是被谁改坏的。

**步骤**：通过`git blame`来查询。

```
git blame app.js

```

> 更多参数请查询`git blame --help`

## 检出历史版本

**场景**：希望将当前项目回到某个历史版本。例如：希望从某个历史版本建立分支时。

**步骤**：`git checkout`

```
# 检出到某个commit，可通过git log得到Commit ID
git checkout 5304f1bd...b4d4
# 检出到某个分支或Tag
git checkout gh-pages

```

> 原则上讲Git历史是不允许更改的，这方面Git很像 [日志结构的文件系统](http://harttle.com/2014/01/03/morden-os-fs.html)（Log-Structured File Systems）。 但也有办法可以更改日志，例如：[寻找并删除Git记录中的大文件](http://harttle.com/2016/03/22/purge-large-files-in-gitrepo.html)