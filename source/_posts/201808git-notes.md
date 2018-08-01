---
title: git-notes
date: 2018-08-01 15:00:19
tags: [git]
categories: 技术
---
## 基础知识
### 介绍
- 版本控制(VCS)是一种记录一个或若干文件内容变化，以便将来查阅特定版本修订情况的系统。
- RCS(Revision Control System)工作原理：在硬盘上保存补丁集（补丁是指文件修订前后的变化）
- CVCS（集中化的版本控制系统）有一个单一的集中管理的服务器，保存所有文件的修订版本，而协同工作的人们都通过客户端连到这台服务器，取出最新的文件或者提交更新。  
	- 缺点：中央服务器的单点故障(e.g. 宕机，磁盘损坏)
- DVCS（分布式版本控制系统）e.g. Git、Mercurial、Bazaar 以及 Darcs等。客户端并不只提取最新版本的文件快照，而是把代码仓库完整地镜像下来。每一次克隆操作，都是对代码仓库的完整备份。  
- 本质上是一个内容寻址（content-addressable）文件系统，并在此之上提供了一个版本控制系统的用户界面。  
**文件目录**：  
	> $ ls -F1  
	HEAD  
	config*  
	description  
	hooks/  
	info/  
	objects/  
	refs/  

<!-- more -->
- `description` 文件仅供 GitWeb 程序使用，我们无需关心。 `config` 文件包含项目特有的配置选项。 `info` 目录包含一个全局性排除（global exclude）文件，用以放置那些不希望被记录在 .gitignore 文件中的忽略模式（ignored patterns）。`hooks` 目录包含客户端或服务端的钩子脚本（hook scripts）。HEAD文件、（尚待创建的）index 文件，和 objects 目录、refs 目录。 这些条目是 Git 的核心组成部分。 `objects` 目录存储所有数据内容；`refs` 目录存储指向数据（分支）的提交对象的指针；`HEAD` 文件指示目前被检出的分支；`index` 文件保存暂存区信息。  



### git基础
- Git对待数据像是一个快照流。每个版本保存最新文件状态，而不是新老文件之间的差异。如果文件没有修改，Git不再重新存储该文件，而是只保留一个链接指向之前存储的文件。  

![Git快照](https://git-scm.com/book/en/v2/images/snapshots.png)  

- Git 用以计算校验和的机制叫做 SHA-1 散列（hash，哈希）。 这是一个由 40 个十六进制字符（0-9 和 a-f）组成字符串，基于 Git 中文件的内容或目录结构计算出来。
- Git三种状态。已提交（committed）、已修改（modified）和已暂存（staged）。 已提交表示数据已经安全的保存在本地数据库中。 已修改表示修改了文件，但还没保存到数据库中。 已暂存表示对一个已修改文件的当前版本做了标记，使之包含在下次提交的快照中。
![Git状态](https://git-scm.com/book/en/v2/images/areas.png)
- 基本的 Git 工作流程如下：  
  1. 在工作目录中修改文件。  
  2. 暂存文件，将文件的快照放入暂存区域。  
  3. 提交更新，找到暂存区域的文件，将快照永久性存储到 Git 仓库目录。  

![文件状态变化周期](https://git-scm.com/book/en/v2/images/lifecycle.png)  
master 默认分支名

文件 .gitignore 的格式规范如下：  

- 所有空行或者以 ＃ 开头的行都会被 Git 忽略。  
- 可以使用标准的 glob 模式匹配。  
- 匹配模式可以以（/）开头防止递归。  
- 匹配模式可以以（/）结尾指定目录。  
- 要忽略指定模式以外的文件或目录，可以在模式前加上惊叹号（!）取反。


### git命令
- 如何配置 Git 来忽略指定的文件和文件模式  
- 如何迅速而简单地撤销错误操作  
- 如何浏览你的项目的历史版本以及不同提交（commits）间的差异  
- 如何向你的远程仓库推送（push）以及如何从你的远程仓库拉取（pull）文件  
- 移除无效的远程仓库
- 管理不同的远程分支并定义它们是否被跟踪

`git config --list` 列出所有git当时能找到的配置    
`git init` 初始化git仓库  
`git clone [url] [custom-repo-name]` 克隆仓库  
Git 支持多种数据传输协议。`https://` 协议，`git://` 协议或者使用 `SSH` 传输协议，比如 user@server:path/to/repo.git  
`git status` 检查当前文件状态    
> `git status -s`和`git status --short`输出更简洁。

`git add` 跟踪新文件。git add 命令使用文件或目录的路径作为参数；如果参数是目录的路径，该命令将递归地跟踪该目录下的所有文件。   
`git diff` 查看尚未暂存的修改  
> `git diff --staged/--cached` 查看已暂存的将要添加到下次提交里的内容  

`git commit -m 'commit message'` 提交更新  
> `git commit -a` 把所有已经跟踪过的文件暂存起来一并提交（跳过`git add`步骤)  
> `git commit --amend -m 'rewrite commit msg'`  

`git rm file/directory` 移除文件  
`git rm --cached file/directory -r` 让文件保留在磁盘，但是并不想让 Git 继续跟踪  
`git log` 查看历史提交记录  
> `git log --pretty=oneline`  pretty选项可指定使用不同于默认格式的方式展示提交历史  
> `git log --pretty=format:"%h - %an, %ar : %s"` [pretty常用选项](https://git-scm.com/book/zh/v2/Git-%E5%9F%BA%E7%A1%80-%E6%9F%A5%E7%9C%8B%E6%8F%90%E4%BA%A4%E5%8E%86%E5%8F%B2#rpretty_format)  
> `git log --date="iso"`  显示具体日期 --date=(relative|local|default|iso|rfc|short|raw) 不能one--oneline一起用     
> `git log -p -2` -p显示每次提交的内容差异 -2显示最近两次提交  
> `git log --stat` 查看提交的简略的统计信息  
> `git log --oneline --decorate --graph --all` 输出提交历史、各个分支的指向以及项目的分支分叉情况

e.g. `git log --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr)%Creset' --abbrev-commit --date=relative`  
`git reset HEAD <file>` 取消暂存的文件  
`git remote -v/show` 查看远程仓库  
`git remote add <shortname> <url>` 添加远程仓库  
`git fetch [remote-name]/origin` 抓取克隆（或上一次抓取）后新推送的所有数据，不会进行合并或修改  
`git pull` 自动抓取然后合并远程分支到当前分支  
`git push origin master` 推动更新到远程仓库  
#### 打标签  
`git tag` 列出标签
`git tag -l 'v1.8.5*'` 查找标签  
Git 使用两种主要类型的标签：轻量标签（lightweight）与附注标签（annotated）。  
`git tag -a v1.4 -m 'my version 1.4'` 创建附注标签  
`git show v1.4` 显示标签信息
`git tag v1.4-lw` 创建轻量标签（不需要使用 -a、-s 或 -m 选项，只需要提供标签名字）  
#### 分支
`git branch [branch-name]` 创建分支，不会自动切换到新分支  
`git checkout -b [branch-name]` 创建分支并同时切换到该分支  
`git log --oneline --decorate` 查看各个分支当前所指的对象  ]
`git checkout [branch-name]` 切换分支（HEAD指向[branch-name]分支） 
`git branch -d [branch-name]` 删除分支 
`git branch` 查看分支列表  
`git branch -v` 查看每一个分支的最后一次提交 
`git merge [branch-name]` 合并分支   
`git branch --merged` 查看哪些分支已经合并到当前分支  
`git branch --no-merged` 查看所有包含未合并工作的分支，使用`git branch -d`命令删除时会失败。可以使用`-D`选项强制删除。  
`git push origin --delete [branch-name]` 删除远程分支  
#### 拉取
`git fetch` 从服务器上抓取本地没有的数据时，它并不会修改工作目录中的内容  
`git merge` 合并  
`git stash/stash save` 储藏工作  
`git stash list` 查看储藏  
`git stash apply/apply stash@{2}` 重新应用（指定）储藏。如果不指定一个储藏，Git 认为指定的是最近的储藏  


### Git分支
首次提交对象及其树结构: 
![首次提交对象及其树结构](https://git-scm.com/book/en/v2/images/commit-and-tree.png)
提交对象及其父对象:
![提交对象及其父对象](https://git-scm.com/book/en/v2/images/commits-and-parents.png)  

`HEAD`指针，指向当前所在的本地分支。   
e.g. 让我们来看一个简单的分支新建与分支合并的例子，实际工作中你可能会用到类似的工作流。 你将经历如下步骤：
> 1. 开发某个网站。  
2. 为实现某个新的需求，创建一个分支。  
3. 在这个分支上开展工作。  

正在此时，你突然接到一个电话说有个很严重的问题需要紧急修补。 你将按照如下方式来处理：  
> 1. 切换到你的线上分支（production branch）。  
2. 为这个紧急任务新建一个分支，并在其中修复它。  
3. 在测试通过之后，切换回线上分支，然后合并这个修补分支，最后将改动推送到线上分支。  
4. 切换回你最初工作的分支上，继续工作。  

`fast-forward` 只将指针向前推进，合并操作没有需要解决的分歧。  
渐进稳定分支的流水线('silo')视图：
![](https://git-scm.com/book/en/v2/images/lr-branches-2.png)  

`rebase` [变基](https://git-scm.com/book/zh/v2/Git-%E5%88%86%E6%94%AF-%E5%8F%98%E5%9F%BA) 是提交到某一分支上的所有修改都移至另一分支上  

### Git协议
Git可以使用四种主要的协议来传输资料：本地协议（local），HTTP协议，SSH(Secure Shell)协议及Git协议。

*Reference:
[git在线文档](https://git-scm.com/book/zh/v2)