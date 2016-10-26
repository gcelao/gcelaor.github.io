---
layout:     post
title:      "Git学习:初始化"
subtitle:   "Learn-Git-Initialization"
date:       2016-10-11 07:40:35
author:     "Gcelaor"
header-img: "img/clound.jpg"
catalog: true
tags:
    - Git
    - Github
---

​     本例子："gcelaor"为我的GitHub用户名，"gcelaor.github.io"是我GitHub上的仓库。

## 从既有远程仓库建立

**场景**：加入一个项目，或创建一个项目副本。

**步骤**：远程仓库已经存在的情况下，直接克隆即可得到一个仓库副本。

```
$ git clone git@github.com:gcelao/gcelaor.github.io
$ cd gcelaor.github.io
```

## 从空的远程仓库建立

**场景**：初始化一个远程仓库，例如建立一个Github仓库后。

**步骤**：新建目录并将其初始化为Git仓库，然后添加远程仓库到`remote`。

```
mkdir bar && cd bar
git init --bare
git remote add origin git@foo.com:bar.git
touch README.md
git add README.md && git commit -m 'init'
# 初次Push需指定远程分支
git push -u origin master
```