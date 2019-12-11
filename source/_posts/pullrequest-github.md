---
title: 如何正确地给 github 的开源项目提交 pull request
date: 2018-01-30 15:51:27
categories: [Git]
tags: [Git,Wiki]
---

1. fork 原始仓库
2. clone 自己的仓库
3. 在 master 分支添加原始仓库为远程分支 git remote add upstream 远程仓库
4. 自己分支开发，如 dev 分支开发：git checkout -b dev
5. 本地 dev 提交
6. 切换 master 分支，同步原始仓库：git checkout master， git pull upstream master
7. 切换本地 dev 分支，合并本地 master 分支（已经和原始仓库同步），可能需要解冲突
8. 提交本地 dev 分支到自己的远程 dev 仓库
9. 现在才是给原始仓库发 pull request 请求
10. 等待原作者回复（接受/拒绝）
