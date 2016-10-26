---
layout:     post
title:      "Git学习:提交代码"
subtitle:   "Learn-Git-Submit-Code"
date:       2016-10-12 09:30:15
author:     "Gcelaor"
header-img: "img/Git.jpg"
catalog: true
tags:
    - Git
    - Github
---

 本文以实际的案例，总结了Git代码提交相关的操作步骤以及涉及到的Git命令。主要包括：

`git add`命令将工作区内容添加到暂存区， `git commit`命令将暂存区内容提交到本地仓库。 添加`-m`参数可直接用指定的message提交本次commit。 否则Vim会打开默认的文本编辑器提示你输入commit message。

## 将改动添加到暂存区

**场景**：在提交前需要选择提交的文件（到暂存区），否则git会提示没有要提交的东西。

**步骤**：使用`git add`命令即可将某个文件（的修改）添加到暂存区。

**文档**：[https://git-scm.com/docs/git-add](https://git-scm.com/docs/git-add)

```
# 添加README.md到暂存区
git add README.md
# 添加当前目录所有文件到暂存区
git add .
# 强制添加，忽略.gitignore配置
git add node_modules/ --force

```

> `git add`会忽略列在`.gitignore`中的文件/目录。

## 提交对仓库中文件的改动

**场景**：希望只提交仓库中既有文件的改动，而不想`add`其他的文件（仓库外）。

**步骤**：省略`git add`命令，然后以`-a`参数运行`commit`。

```
git commit -a

```

> 可通过`git status`来查看当前的改动情况，以及本地与远程的同步情况。

## 撤销Add

**场景**：不小心添加了文件到暂存区，现在需要撤销所有的`git add`。

**步骤**：使用`get reset`，重置暂存区到HEAD。

```
# 取消Add某一个文件
git reset path/to/file
# 取消所有Add的文件（将会使得所有改动变成not staged或untracked）
git reset

```

## 撤销上次Commit

**场景**：发现上次`commit`信息有误，或不小心`commit`了不合适的文件， 希望能撤销`commit`而文件不受改动。

**步骤**：使用Git的『软』（不改动文件）重置。

```
git reset --soft HEAD^

```

> `HEAD^`回到表示重置到当前状态的前一个`commit`。

## 修改上次Commit

**场景**：漏掉了某个文件，或者写错了Commit信息，希望能够补充一下而不是撤销再重新Commit。

**步骤**：使用`--amend`参数即可修改上次Commit。

**文档**：[https://git-scm.com/book/zh/v1/Git-%E5%9F%BA%E7%A1%80-%E6%92%A4%E6%B6%88%E6%93%8D%E4%BD%9C](https://git-scm.com/book/zh/v1/Git-%E5%9F%BA%E7%A1%80-%E6%92%A4%E6%B6%88%E6%93%8D%E4%BD%9C)

```
# 下面三条命令只产生一个Commit
git commit -m 'initial commit'
git add forgotten_file  # 添加漏掉的文件
git commit --amend      # 补充Commit信息

```

## 撤销工作区所有改动

**场景**：希望撤销所有工作区的改动，回到最后一次commit的状态。

**步骤**：`git checkout`和`git reset`都可达到目的。

**文档**：[https://git-scm.com/docs/git-reset](https://git-scm.com/docs/git-reset), [https://git-scm.com/docs/git-checkout](https://git-scm.com/docs/git-checkout)

```
# 重置工作区的所有改动
git reset --hard
# 该命令可以指定当前目录，还是某个文件
git checkout .

```

## 空提交

**场景**：只想产生一个commit而不想改动文件。比如需要push一个commit以触发重新部署的Git Hook时。 **步骤**：使用`--allow-empty`参数来提交。

```
git commit --allow-empty -m 'empty commit'

```

## 将文件从仓库中移除

**场景**：不小心把不应提交到仓库的文件（比如临时文件，大文件，配置文件等）提交了进去，现在希望将其删除。

**步骤**：使用 `git rm` 命令。

```
# 从仓库和工作区都删除它（例如临时文件）
git rm .*.swp
# 只从仓库中删除，工作区中保留（例如配置文件）
git rm --cached config.yml

```

如果希望从仓库历史中也删除（例如大文件），那么需要使用`git filter-branch`系列命令。 请参考[寻找并删除Git记录中的大文件](http://harttle.com/2016/03/22/purge-large-files-in-gitrepo.html)一文。

> `git rm`和bash `rm`的参数类似，基本可通用。