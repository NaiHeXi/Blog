---
title: Git教程
date: 2021-12-22 18:46:19
author: 奈何
tags: git
categories: Tools
---

<div align='center' ><font size='8'>Git教程</font></div>

# Git介绍

git命令思维导图：

![git1](https://naihexi.gitee.io/picgo/blog/git1.png)

1.  **分布式**：Git版本控制系统是一个分布式的系统，是用来保存工程源代码历史状态的命令行工具。

2.   **保存点**：Git的保存点可以追踪源码中的文件, 并能得到某一个时间点上的整个工程项目的状态；可以在该保存点将多人提交的源码合并, 也可以回退到某一个保存点上。

3.   **Git离线操作性**：Git可以离线进行代码提交，因此它称得上是完全的分布式处理，Git所有的操作不需要在线进行；这意味着Git的速度要比SVN等工具快得多，因为SVN等工具需要在线时才能操作，如果网络环境不好， 提交代码会变得非常缓慢。

4.   **Git****基于快照**：SVN等老式版本控制工具是将提交点保存成补丁文件，Git提交是将提交点指向提交时的项目快照，提交的东西包含一些元数据(作者，日期，GPG等)。

5.   **Git****的分支和合并**：分支模型是Git最显著的特点，因为这改变了开发者的开发模式，SVN等版本控制工具将每个分支都要放在不同的目录中，Git可以在同一个目录中切换不同的分支。

6.   **分支即时性**：创建和切换分支几乎是同时进行的，用户可以上传一部分分支，另外一部分分支可以隐藏在本地，不必将所有的分支都上传到GitHub中去。

7.   **分支灵活性**：用户可以随时创建、合并、删除分支，多人实现不同的功能，可以创建多个分支进行开发，之后进行分支合并，这种方式使开发变得快速、简单、安全。

# Git工作流程

1.   从远程仓库中克隆 Git 资源作为本地仓库。

2.   从本地仓库中checkout代码然后进行代码修改

3.   在提交前先将代码提交到暂存区。

4.   提交修改。提交到本地仓库。本地仓库中保存修改的各个历史版本。

5.   在修改完成后，需要和团队成员共享代码时，可以将代码push到远程仓库。

![git2](https://naihexi.gitee.io/picgo/blog/git2.jpg)

# Git安装

​	官网下载地址：https://git-scm.com/download

## Windows

下载相应git版本，默认安装即可

![git3](https://naihexi.gitee.io/picgo/blog/git3.jpg)

​	默认使用Git Bash即可

![git4](https://naihexi.gitee.io/picgo/blog/git4.jpg)

选择提交的时候换行格式

（1）检查出windows格式转换为unix格式：将windows格式的换行转为unix格式的换行再进行提交。

（2）检查出原来格式转为unix格式：不管什么格式的，一律转为unix格式的换行再进行提交。

（3）不进行格式转换 : 不进行转换，检查出什么，就提交什么。

## Linux

```sh
sudo apt-get install git
```

## 常用配置

### 用户、邮件配置

```sh
#1、查询当前的Git配置
git config --list
#2、编辑Git配置文件
git config -e [--global]
#3、配置邮箱、有户名
git config --global user.email "666.com"
git config --global user.name "rain"
```

### 设置大小写敏感

​	Windows上的Git默认是大小写不敏感的。

```sh
git config core.ignorecase false
```



# 远程仓库

## GitHub

### 创建仓库

![git5](https://naihexi.gitee.io/picgo/blog/git5.jpg)

### SSH

Github支持两种同步方式`“https”`和`“ssh”`。

如果使用`https`很简单基本不需要配置就可以使用，但是每次提交代码和下载代码时都需要输入用户名和密码。

如果使用`ssh`方式就需要客户端先生成一个密钥对，即一个公钥一个私钥。然后还需要把公钥放到githib的服务器上。

SSH（Secure Shell）：安全外壳协议

#### 基于密匙的安全验证

>   ​	使用ssh协议通信时，推荐使用基于密钥的验证方式。你必须为自己创建一对密匙，并把公用密匙放在需要访问的服务器上。
>   ​	如果你要连接到SSH服务器上，客户端软件就会向服务器发出请求，请求用你的密匙进行安全验证。服务器收到请求之后，先在该服务器上你的主目录下寻找你的公用密匙，然后把它和你发送过来的公用密匙进行比较。
>   ​	如果两个密匙一致，服务器就用公用密匙加密“质询”（challenge）并把它发送给客户端软件。
>   ​	客户端软件收到“质询”之后就可以用你的私人密匙解密再把它发送给服务器。

#### ssh密钥生成

Windows下ssh秘钥路径：**C:\Users\用户名\\.ssh**

秘钥文件：

​	**id_rsa** 			   私钥

​	**id_rsa.pub**		公钥

如果没有秘钥文件，就打开命令行工具生成：

```bash
ssh-keygen -t rsa
```

#### ssh密钥配置

进入 Settings 页面：

![git6](https://naihexi.gitee.io/picgo/blog/git6.jpg)

​	在key部分将 **id_rsa.pub** 文件内容添加进去，然后点击 “Add SSH key” 按钮完成配置。

#### ssh多个私钥管理

​	使用本地托管多个个ssh的密钥，不同的账号用不同的密匙。

##### 生成SSH Key

```bash
# 1、Creates a new ssh key using the provided email Generating public/private rsa key pair.
$ ssh-keygen -t rsa -C "your_email@youremail.com"
# 2、输入将要保存的路径，我的默认为当前路径（/c/Users/liutl/.ssh/id_rsa）,但是不能使用默认文件id_rsa，要添加新账户就要生起一个成新的好记的名字，例如id_rsa_work
Enter file in which to save the key (/c/Users/zhaoyafei/.ssh/id_rsa):
# 3、输入回车后提示输入一个类似于密码的号，直接回车
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
```

##### 识别新的私钥

​	默认SSH只会读取id_rsa，所以为了让SSH识别新的私钥，需要将其添加到SSH agent。

```bash
$ ssh-add ～/.ssh/id_rsa_work
#该命令如果报错：Could not open a connection to your authentication agent.
# 依次执行命令，看是否成功
ssh-agent bash 
ssh-add -l 
```

##### 修改config文件

-   **Linux**

1.  **/etc/.gitconfig** 文件：包含了适用于系统所有用户和所有库的值。传递参数选项’--system’ ，读和写这个文件。
2.  **~/.gitconfig** 文件 ：具体到用户。传递--global 选项使Git 读或写这个特定的文件。
3.  **.git/config**文件：局部配置文件，在.git/config中的值覆盖了在/etc/gitconfig中的同一个值。

该文件用于配置私钥对应的服务器。

```bash
# Default github （默认的）
Host github.com
HostName github.com
User git
IdentityFile ~/.ssh/id_rsa

# second user(work@gmail.com)
Host github_work
HostName github.com
User git
IdentityFile ~/.ssh/id_rsa_work
```

​	这样配置，也就是使用hostname为github.com会根据用户名的不同，去使用不用的private key。github上，也可以添加对应的公钥。

-   **Windows**

​	Git在$HOME目录中查找.gitconfig文件（通常位于C:\Documents and Settings\$USER下）。

##### **将SSH key输入到GitHub网站中** 

​	将生成的id_rsa_work.pub输入到GitHub网站中。

**注意：**github根据配置文件的user.email来获取github帐号显示author信息，所以对于多帐号用户一定要记得将user.email改为相应的email

```bash
# 设置局部的user.name和user.email
git config user.name "xxxxxx"
git config user.email "xxx@xxx.com"
```



# Git常用命令

## 命令列表

```sh

```

## 版本管理

### 远程同步

#### 查看状态

```sh
# 显示所有远程仓库
git remote -v
# 显示某个远程仓库的信息
git remote show [remote]

```

#### 从远程仓库克隆

```sh
# 增加一个新的远程仓库，并命名
git remote add [shortname] [url]
# 克隆远程仓库
git clone [git.url]
# 下载远程仓库的所有变动
git fetch [remote]
```

#### 从远程仓库拉取

```sh
# 取回远程仓库的变化，并与本地分支合并
git pull [remote] [branch]
```

#### 推送到远程仓库

```sh
git push <remote 名字> <本地分支的名字> : <远程库的名字>
git push origin HEAD:refs/for/master
# origin : 是远程的库的名字
# HEAD: 是一个特别的指针，它是一个指向你正在工作的本地分支的指针，可以把它当做本地分支的别名，git这样就可以知道你工作在哪个分支
# refs/for :意义在于我们提交代码到服务器之后是需要经过code review 之后才能进行merge的
# refs/heads 不需要经过code review


# 上传本地指定分支到远程仓库（初次更新加-u）
git push (-u) [remote] [branch]
# 强行推送当前分支到远程仓库，即使有冲突，慎用
git push [remote] --force
# 推送所有分支到远程仓库
git push [remote] --all
```

#### 关联远程仓库

```sh
#1、把这个目录变成git可以管理的仓库
git init
#2、添加远程仓库
git remote add origin [git.url]
#3、本地仓库与远程仓库关联
git branch –-set-upstream-to=origin/master master
```

### 查看命令

#### 查看状态

```sh
# 显示有变更的文件
git status
# 显示指定文件是什么人在什么时间修改过
git blame [file]
# 显示某次提交的元数据和内容变化
git show [commit]
# 显示某次提交发生变化的文件
git show --name-only [commit]
# 显示某次提交时，某个文件的内容
git show [commit]:[filename]
# 显示当前分支的最近几次提交
git reflog
```

#### 查看日志

```sh
# 显示当前分支的版本历史
git log
# 显示commit历史，以及每次commit发生变更的文件
git log --stat
# 搜索提交历史，根据关键词
git log -S [keyword]
# 显示某个commit之后的所有变动，每个commit占据一行
git log [tag] HEAD --pretty=format:%s
# 显示某个commit之后的所有变动，其"提交说明"必须符合搜索条件
git log [tag] HEAD --grep feature
# 显示某个文件的版本历史，包括文件改名
git log --follow [file]
git whatchanged [file]
# 显示指定文件相关的每一次diff
git log -p [file]
# 显示过去5次提交
git log -5 --pretty --oneline
# 显示所有提交过的用户，按提交次数排序
git shortlog -sn
```

#### 查看差异

```sh
# 显示暂存区和工作区的差异
git diff
# 显示暂存区和上一个commit的差异
git diff --cached [file]
# 显示工作区与当前分支最新commit之间的差异
git diff HEAD
# 显示两次提交之间的差异
git diff [first-commit] [second-commit]
# 显示今天你写了多少行代码
git diff --shortstat "@{0 day ago}"
```



#### 

```sh
#1、查看仓库状态
git status
#2、查看X文件修改了那些内容
git diff  *   
#3、查看历史记录
git log
#4、查看历史记录的版本号id（记录每一次命令,不论是否提交）
git reflog
#5、如果信息量太多可以进行比较好的列表显示
git log --pretty=oneline    
```



### 撤销

#### reset

​	撤销某次提交，但是此次之后的修改都会被退回到暂存区，把HEAD向后移动了一下。

```sh
# 重置暂存区的指定文件，与上一次commit保持一致，但工作区不变
git reset [file]
# 重置暂存区与工作区，与上一次commit保持一致
git reset --hard
# 重置当前分支的指针为指定commit，同时重置暂存区，但工作区不变
git reset [commit]
# 重置当前分支的HEAD为指定commit，同时重置暂存区和工作区，与指定commit一致
git reset --hard [commit]
# 重置当前HEAD为指定commit，但保持暂存区和工作区不变
git reset --keep [commit]
# 回退到第几个版本
git reset --hard HEAD~N
```

#### revert

​	用一次新的commit来回滚之前的commit，HEAD继续前进。

```sh
# 新建一个commit，用来撤销指定commit，后者的所有变化都将被前者抵消，并且应用到当前分支
git revert [commit]
#
git revert –hard a167
```

#### checkout

```sh
# 恢复暂存区的指定文件到工作区（撤销未提交的修改）
git checkout [file]
git checkout -- [file]
# 恢复某个commit的指定文件到暂存区和工作区
git checkout [commit] [file]
# 恢复暂存区的所有文件到工作区
git checkout .
```

#### stash

```sh
# 暂时将未提交的变化移除，稍后再移入
git stash
git stash pop
```

### 添加文件

```sh
# 1、添加指定文件到暂存区
git add [file1] [file2] ...
# 2、添加指定目录到暂存区，包括子目录
git add [dir]
# 3、添加当前目录的所有文件到暂存区，慎用
git add .
# 4、对于同一个文件的多处变化，可以实现逐块分次提交
git add -p file
```

### 提交

#### 提交到本地库

```sh
# 1、提交暂存区到仓库区
git commit -m [message]
# 2、提交暂存区的指定文件到仓库区
git commit [file1] [file2] ... -m [message]
# 3、提交工作区自上次commit之后的变化，直接到仓库区
git commit -a
# 4、提交时显示所有diff信息
git commit -v
```

#### 追加修改

```sh
# 1、使用一次新的commit，替代上一次提交 
# 如果代码没有任何新变化，则用来改写上一次commit的提交信息
git commit --amend -m [message]
# 2、重做上一次commit，并包括指定文件的新变化
git commit --amend [file1] [file2] ...
```



#### 提交到远程库

### 删除

#### 删除工作区文件

```sh
# 删除工作区文件，并且将这次删除放入暂存区
git rm [file1] [file2] ...
```

#### 停止追踪指定文件

```sh
# 停止追踪指定文件，但该文件会保留在工作区
git rm --cached [file]
```

#### 改名文件

```sh
# 改名文件，并且将这个改名放入暂存区
git mv [file-original] [file-renamed]
```

#### 删除未添加到版本中的文件或者文件夹

```sh
# 删除 untracked files
git clean -f 
# 连 untracked 的目录也一起删掉
git clean -fd
# 连 gitignore的untrack 文件/目录也一起删掉 （一般这个是用来删掉编译出来的 .o一类的文件）
git clean -xfd
# 在使用清理 git clean之前，建议加上 -n 来先看看会删掉哪些文件，防止重要文件被误删
git clean -nxfd
git clean -nf
git clean -nfd
```

### 隐藏的文件

```sh
#1、把当前的工作隐藏起来 等以后恢复现场后继续工作
git stash
#2、查看所有被隐藏的文件列表
git stash list
#3、恢复被隐藏的文件，但是内容不删除
git stash apply
#4、删除文件
git stash drop
#5、恢复文件的同时 也删除文件
git stash pop
```



## 分支管理

### 查看分支

```sh
# 1、查看本地所有的分支
git branch
# 2、查看远程分支,本地和远程
git branch -a
# 3、列出所有远程分支
git branch -r
```

### 创建分支

```sh
# 1、新建一个分支，但依然停留在当前分支
git branch [branch-name]
# 2、新建一个分支，并切换到该分支
git checkout -b [branch-name]
# 3、新建一个分支，指向指定commit
git branch [branch] [commit]
# 4、新建一个分支，与指定的远程分支建立追踪关系
git branch --track [branch] [remote-branch]
# 5、重命名分支
git branch -m dev [branch-name]
# 6、建立追踪关系，在现有分支与指定的远程分支之间
git branch --set-upstream [branch] [remote-branch]
```

### 删除分支

```sh
#1、删除分支
git branch -d [branch-name]
#2、删除远程的dev分支
git push origin --delete [branch-name]
git branch -dr [remote/branch]
```

### 切换分支

```sh
# 切换到指定分支，并更新工作区
git checkout [branch-name]
# 切换到上一个分支
git checkout -
```

### 推送分支

```sh
#1、把当前新增的dev分支推送到远程库(远程仓库没有该分支则会新建立该分支)
git push origin dev
#2、提交修改并创建远程分支dev
git push --set-upstream origin dev
```



### 拉取分支

```sh
#方法一
git checkout -b   本地分支名x origin/远程分支名x
#方法二
git fetch origin  远程分支名x:本地分支名x
# clone到指定目录
git clone xxx.git "指定目录"
# clone时创建新的分支替代默认Origin HEAD（master）
git clone -b branchname xxx.git
```



### 合并分支

```sh
# 1、合并指定分支到当前分支
git merge [branch]
# 2、选择一个commit，合并进当前分支
git cherry-pick [commit]
```

​	通常合并分支时，git一般使用`”Fast forward”`模式，在这种模式下，删除分支后，会丢掉分支信息，现在我们来使用带参数 –no-ff来禁用`”Fast forward”`模式。

```sh
git merge –-no-ff -m “注释” dev
```

合并过程：

```sh
#1、切换到develop分支
git checkout develop
#2、把develop分支代码拉取到本地
git pull
#3、切换到master主干
git checkout master
#4、合并develop分支代码到master
git merge develop
#5、提交到远程master主干
git push
```

#### 冲突解决

​	根据提示冲突文件解决冲突。

## 标签管理

### 查看tag

```sh
# 列出所有tag
git tag
# 查看tag信息
git show [tag]
```

### 新建tag

```sh
# 新建一个tag在当前commit
git tag [tag]
# 新建一个tag在指定commit
git tag [tag] [commit]
# 新建一个分支，指向某个tag
git checkout -b [branch] [tag]
```

### 提交tag

```sh
# 提交指定tag
git push [remote] [tag]
# 提交所有tag
git push [remote] --tags
```

### 删除tag

```sh
# 删除本地tag
git tag -d [tag]
# 删除远程tag
git push origin :refs/tags/[tagName]
```

## 其它

```sh
# 生成一个可供发布的压缩包
git archive
```

## Git分支管理策略

### 主分支Master

​	代码库应该有一个、且仅有一个主分支。所有提供给用户使用的正式版本，都在这个主分支上发布。

![git7](https://naihexi.gitee.io/picgo/blog/git7.png)

​	Git主分支的名字，默认叫做Master。它是自动建立的，版本库初始化以后，默认就是在主分支在进行开发。

### 开发分支Develop

​	主分支只用来分布重大版本，日常开发应该在另一条分支上完成。把开发用的分支，叫做Develop。

![git8](https://naihexi.gitee.io/picgo/blog/git8.png)

​	这个分支可以用来生成代码的最新隔夜版本（nightly）。如果想正式对外发布，就在Master分支上，对Develop分支进行"合并"（merge）。

```sh
# 创建Develop分支
git checkout -b develop master
# 切换到Master分支
git checkout master
# 对Develop分支进行合并
git merge --no-ff develop
```

​	默认情况下，Git执行"快进式合并"（fast-farward merge），会直接将Master分支指向Develop分支。

![git9](https://naihexi.gitee.io/picgo/blog/git9.png)

​	使用--no-ff参数后，会执行正常合并，在Master分支上生成一个新节点。

![git10](https://naihexi.gitee.io/picgo/blog/git10.png)

### 临时性分支】

临时性分支，用于应对一些特定目的的版本开发。临时性分支主要有三种：

```
　* 功能（feature）分支
　* 预发布（release）分支
　* 修补bug（fixbug）分支
```

#### 功能分支

​	功能分支，是为了开发某种特定功能，从Develop分支上面分出来的。开发完成后，要再并入Develop。

![git11](https://naihexi.gitee.io/picgo/blog/git11.png)

```sh
# 创建一个功能分支：
git checkout -b feature-x develop
# 开发完成后，将功能分支合并到develop分支：
git checkout develop
git merge --no-ff feature-x
# 删除feature分支：
git branch -d feature-x
```

#### 预发布分支

​	预发布分支，是指发布正式版本之前（即合并到Master分支之前），可能需要有一个预发布的版本进行测试。

​	预发布分支是从Develop分支上面分出来的，预发布结束以后，必须合并进Develop和Master分支。

```sh
# 创建一个预发布分支：
git checkout -b release-1.2 develop
# 确认没有问题后，合并到master分支：
git checkout master
git merge --no-ff release-1.2
# 对合并生成的新节点，做一个标签
git tag -a 1.2
# 再合并到develop分支：
git checkout develop
git merge --no-ff release-1.2
#最后，删除预发布分支：
git branch -d release-1.2
```

#### 修补bug分支

​	修补bug分支。软件正式发布以后，难免会出现bug。这时就需要创建一个分支，进行bug修补。

​	修补bug分支是从Master分支上面分出来的。修补结束以后，再合并进Master和Develop分支。

![git12](https://naihexi.gitee.io/picgo/blog/git12.png)

```sh
# 创建一个修补bug分支：
git checkout -b fixbug-0.1 master
# 修补结束后，合并到master分支：
git checkout master
git merge --no-ff fixbug-0.1
git tag -a 0.1.1
# 再合并到develop分支：
git checkout develop
git merge --no-ff fixbug-0.1
# 最后，删除"修补bug分支"：
git branch -d fixbug-0.1
```

## 忽略文件 .gitignore

​	.gitignore 配置文件用于配置不需要加入版本管理的文件。

配置语法：

​	"/" 开头表示目录；
​	"?" 通配单个字符；
​	"[]" 包含单个字符的匹配列表；
​	"!" 表示不忽略(跟踪)匹配到的文件或目录；
​	说明：git 对于 .ignore 配置文件是按行从上到下进行规则匹配的，意味着如果前面的规则匹配的范围更大，则后面的规则将不会生效；

编辑 .gitignore 文件：

```sh
# 1、忽略目录foder下的全部内容（根目录、某个子目录）
foder/* 
# 2、忽略根目录下的 /foder/ 目录的全部内容
/foder/*
#忽略全部内容，但是不忽略 .gitignore文件,根目录下的 /fw/bin/ 和 /fw/sf/ 
/*!.gitignore
!/fw/bin/
!/fw/sf/
```

注意问题： .gitignore文件只对还没有加入版本管理的文件起作用，如果之前已经用git把要忽略的文件纳入了版本库，就不起作用了。

## git 打补丁

### patch与diff

-   .diff：git diff生成的UNIX标准补丁文件，只记录文件改变的内容，不带有commit记录信息,多个commit可以合并成一个diff文件。 
-   .patch：git format-patch生成的Git专用.patch 文件，带有记录文件改变的内容，也带有commit记录信息,每个commit对应一个patch文件。

### 创建patch与diff

#### 创建patch文件

```shell
#1、某次提交（含）之前的几次提交的patch
git format-patch 【commit sha1 id】-n
#2、某两次提交之间的所有patch
git format-patch 【commit sha1 id】..【commit sha1 id】
```

#### 创建diff文件

```shell
git diff  【commit sha1 id】 【commit sha1 id】 >  【diff文件名】
```

### 应用patch与diff

-   检查patch/diff是否能正常打入

    ```sh
    git apply --check 【path/to/xxx.patch】
    git apply --check 【path/to/xxx.diff】
    ```

-   打入patch/diff

    ```shell
    git apply 【path/to/xxx.patch】
    git apply 【path/to/xxx.diff】
    #或者
    git am 【--s --signoff】 【path/to/xxx.patch】
    git am 【--whitespace=fix】 【path/to/xxx.patch】
    ```

### 冲突解决

-   使用 以下命令行，自动合入 patch 中不冲突的代码改动，同时保留冲突的部分：

    ```shell
    git  apply --reject  xxxx.patch
    ```

    同时会生成后缀为 .rej 的文件，保存没有合并进去的部分的内容，可以参考这个进行冲突解决。

-   解决完冲突后删除后缀为 .rej 的文件，并执行`git add.`添加改动到暂存区.

-   继续冲突合入

    ```shell
    git am --resolved
    #或者
    git am --continue
    ```

合入冲突：	

```shell
# 跳过此次冲突，也可以执行
git am --skip
#回退打入patch的动作，还原到操作前的状态
git am --abort
```

## 更改某个提交内容

可以创建一个分支，用于rebase:

```bash
git checkout -b rebase_tmp
```

**rebase 要指定parent commitID**。

### 直接更改某次提交

```bash
# 1、HEAD移到需要更改的commit上:
git rebase -i 0bdf89^
# 1.1、弹出的交互式界面中显示的commit 信息，找到需要更改的commit, 将行首的pick改成edit, 按esc, 输入:wq退出
# 2、更改文件
# 3、添加改动文件到暂存
git add file_mod
# 4 追加改动到第一步中指定的commit上
git commit --amend
# 5、移动HEAD到最新的commit处
git rebase --continue
# 6、解决冲突:
	# 6.1、编辑冲突文件, 解决冲突
    # 6.2、添加修改冲突文件到暂存
    git add .
    # 6.3、追加改动到上一步中指定的commit上
    git commit --amend
	# 6.4、解决冲突之后移动HEAD到最新的commit处
	git rebase --continue
```

### 将工作空间中的改动追加到某次提交上

```bash
# 1、保存工作空间中的改动
git stash
# 2、将HEAD移到需要更改的commit上:
git rebase f744c32^ --interactive
# 2.1、弹出的交互式界面中显示的commit 信息，找到需要更改的commit, 将行首的pick改成edit, 按esc, 输入:wq退出
# 3、执行命令
git stash pop
# 4、添加改动文件到暂存
git add file_mod
# 5、追加改动到第一步中指定的commit上
git commit --amend
# 6、移动HEAD到最新的commit处
git rebase --continue
# 7、解决冲突:
    # 7.1、编辑冲突文件, 解决冲突
    # 7.2、添加修改冲突文件到暂存
    git add .
    # 7.3、追加改动到上一步中指定的commit上
    git commit --amend
	# 7.4、解决冲突之后移动HEAD到最新的commit处
	git rebase --continue
```



# Git常见问题

## window与linux的换行符问题

```shell
git config --global core.autocrlf false
git config --global core.filemode false
git config --global core.safecrlf true
```

**AutoCRLF**：

```shell
#提交时转换为LF，检出时转换为CRLF
git config --global core.autocrlf true  
#提交时转换为LF，检出时不转换
git config --global core.autocrlf input  
#提交检出均不转换
git config --global core.autocrlf false
```

## 修改文件权限后文件状态修改

```shell
#1、修改文件夹权限
chmod -R 755 test_dir
#2、查看 git 仓库状态，提示文件夹下所有文件被修改
git status
#3、配置文件模式，忽略文件或文件夹权限修改，解决
git config core.filemode false
```

## 拉取仓库中某个目录

```sh
#1、开启 Git 的稀疏签出功能, 开启之后方能限制 pull Or push 时规定的某一个目录
git config core.sparsecheckout true
#2、配置需检出的目录
echo firstDir/* >> .git/info/sparse-checkout
```



## Github访问速度慢

优化思路：通过绕过DNS解析，直接在本地绑定host

### 查询DNS

DNS查询网站：

​	**https://www.ipaddress.com/**

​	**http://tool.chinaz.com/dns**

查询 github 相关网址域名

```
github.com
github.global.ssl.fastly.net
```

### 修改hosts

windows下打开文件：C:\Windows\System32\drivers\etc\hosts

末尾追加内容：

```shell
140.82.112.3 github.com
199.232.69.194 github.global.ssl.fastly.net
```

### 刷新DNS

windows下刷新DNS：

```shell
ipconfig /flushdns
```

## 切换git 命令提示中文到英文

```sh
#出现全中文的提示，切换到中文
#1:写入
echo "alias git='LANG=en_GB git'" >> ~/.bashrc
#2:生效
source ~/.bashrc
```

## git push警告

![git13](https://naihexi.gitee.io/picgo/blog/git13.png)

解决办法：‘matching’ 参数是 Git 1.x 的默认行为，如果你执行 git push 但没有指定分支，它将 push  所有你本地的分支到远程仓库中对应匹配的分支。而 Git 2.x 默认的是 simple，意味着执行 git push  没有指定分支时，只有当前分支会被 push 到你使用 git pull 获取的代码。 
     根据提示，修改git push:

```sh
git config --global push.default matching
```

再次执行git push。

## 当前分支没有追踪信息

**There is no tracking information for the current branch...**
则说明本地分支和远程分支的链接关系没有创建，用命令：

```sh
git branch --set-upstream branch-name origin/branch-name
```

## 冲突，推送失败

 **![rejected] dev -> dev (non-fast-forward) ... Updates were rejected because the tip of your current branch**
     推送失败，因为远程代码的最新提交和你试图推送的提交有冲突，解决办法：

​	先用git pull把最新的提交从origin/dev抓下来，然后，在本地合并，解决冲突，再推送。

## OpenSSL SSL_read

OpenSSL SSL_read: Connection was reset, errno 10054 

修改设置，解除ssl验证

```sh
git config --global http.sslVerify false
```

## 不能追踪某个文件夹下的修改

fatal: Pathspec 'xxx' is in submodule

```bash
git rm -rf --cached folder
```

## 检测不到文件变化

​	git 提交之后，在git上某个文件有后缀@b4c4u7之类的。

​	本地 git [status](https://so.csdn.net/so/search?q=status&spm=1001.2101.3001.7020) 的时候检测不到文件的变化：

```shell
# 从.git/index中删除所有变更过的文件最后再正常提交
git rm -r --cached . 
git add .
git commit -m "Initial commit"
git push origin master
```



# Git - svn

SVN是集中式版本控制系统，版本库是集中放在中央服务器的。

Git是分布式版本控制系统，那么它就没有中央服务器的，每个人的电脑就是一个完整的版本库。

## 安装

```sh
sudo apt-get install git-svn
```

## 下载svn代码

```sh
git svn clone url
```

这个操作会从第一个版本开始同步，若版本迭代太多会很费时，优化处理是检出最近的n个版本：

```sh
#1、查询最后的版本号为 No
svn info url
#2、检出最近 n 个版本，检出开始版本号为 m=No-n
git svn clone -r m:HEAD url
```

## 更新svn仓库到本地

```sh
git svn rebase
```

## 本地修改提交到svn仓库

```sh
git svn dcommit
```

## 提交冲突解决

```sh
#0、提交发生冲突
git svn dcommit
#1、获取svn服务器上的最新冲突文件
git svn rebase
#2、打开冲突文件，修改代码，解决冲突
git rebase –continue
#3、告知git已完成冲突解决
git add conflict.c
#4、再次检查冲突
git rebase –continue
#5、查看日志
git log
#6、再次提交
git svn dcommit
```

## 查看log

```sh
#1、显示每次修改提交的文件
git svn log -v
#2、查看提交日志
git log
#3、可以查看每次提交log和对应的修改内容
git log -p
#4、查看每次提交log和对应的修改文件
git log --stat (可以查看每次提交log和对应的修改文件)
#5、查看某人的log
git log --author=
```

# svn

## 常用命令

```bash
#svn常命令
svn blame (praise, annotate, ann)
svn changelist (cl)
svn cleanup
svn copy (cp)
svn export
svn import
svn lock
svn mergeinfo
svn mkdir
svn move (mv, rename, ren)
svn propdel (pdel, pd)
svn propedit (pedit, pe)
svn propget (pget, pg)
svn proplist (plist, pl)
svn propset (pset, ps)
svn resolved
svn switch (sw)
svn unlock
```

### 添加

```bash
# 添加文件或目录
svn add file|dir
```

### 拉取代码

```bash
# 获取svn代码
svn co	# 简写
svn checkout
```

### 更新

```bash
svn up	# 简写
svn update
```

### 提交

```bash
# 提交代码修改
svn ci	# 简写
svn commit -m 指定提交修改备注
```

### 删除文件

```bash
svn delete (del, remove, rm)
```

### 撤销

```bash
# 撤销本地修改
svn revert
```

### 合并

```bash
# 合并svn和本地代码
svn merge
# 合并冲突代码
svn resolve
```

### 查看

#### 查看状态

```bash
# 查看本地修改情况：列出本地修改或增加的文件信息
svn st/stat	# 简写
svn status
```

>   “ ” 无修改
>
>   “A” 新增
>   “C” 冲突
>   “D” 删除
>   “G” 合并
>   “I” 忽略
>   “M” 改变
>   “R” 替换
>   “X” 未纳入版本控制，但被外部定义所用
>   **“?”** 未纳入版本控制
>   **“!”** 该项目已遗失 (被非 svn 命令所删除) 或是不完整

#### 查看日志

```bash
# 查看提交日志
svn log -l number 指定只显示最近的几条日志
```

#### 查看信息

```bash
# 查看当前的svn信息，会显示svn库的URL，最新版本和最后提交时间
svn info
```

#### 查看差异

```bash
# 将本地代码和svn上进行对比，可指定文件
svn di	# 简写
svn diff
# 比较本地文件和某版本号此文件
svn diff -r 版本号 文件名
# 比较版本23和版本24
svn diff -r 23:24
# 比较某文件的版本23和版本24
svn diff -r 23:24  文件名
```

#### 查看指定版本某文件内容

```bash
# 显示特定版本的某文件内容
svn cat -r 版本号 文件名
```

#### 查看目录列表

```bash
# 显示svn下目录列表
svn list(ls)
# 查看每一个目录最后更新的人、版本、时间
svn list -v
```

#### 查看帮助

```bash
# 查看svn帮助，或特定命令帮助
svn help [command]
```

### 属性

#### 获取属性

```bash
svn propget(pg,pget)
```

#### 设置属性

```bash
svn propset(ps,pset)
# -F [--file] ARG	：从文件 ARG 读取属性值
svn ps svn:ignore -F .svnignore .
```

#### 编辑属性

```bash
svn propedit(pe,pedit) svn:ignore 目录名称
```

#### 恢复属性

​	在不影响内容更改的情况下还原所有属性更改：

```bash
svn revert `svn status | grep '^ M' | sed 's/^ M \+//g'`
```



## 忽略不必要的文件和文件夹

**propset(ps,pset)** 用于设置属性的值；**propget(pg,pget) **用于获取属性的值。

​	**svn pg svn:ignore  #获取属性值**

​	**svn ps svn:ignore 'value' path #设置属性值**

### 忽略文件夹

```bash
# 1.配置SVN默认编辑器
vi ~/.bash_profile
# 最后一行加上：
export SVN_EDITOR=vim  # 定义svn editor为vim编辑
# 2.让配置生效
source ~/.bash_profile
# 3.忽略当前路径下test文件夹
svn propset svn:ignore 'test' ./
property 'svn:ignore' set on '.'
# 4.使用 -R 递归属性配置，子文件夹也进行忽略 
svn propset svn:ignore -R *.class .
```

>   设置忽略目录或文件：
>   	svn propedit svn:ignore . #最后的点号表示当前目录不能少
>     	此时会打开vim编辑器，编辑这个文件，即告诉svn哪些目录或者目录应该被忽略，可能会有报错：
>      	svn: None of the environment variables SVN_EDITOR, VISUAL or EDITOR  are set, and no 'editor-cmd' run-time configuration option was found
>     	说明没有给svn的忽略目录设置文件指定使用什么来编辑，可执行如下命令，或者将这行命令写入到启动脚本: **~/.bash_profile** 中
>     		export SVN_EDITOR=vim
>     	也可以直接修改SVN的配置文件：修改这行为：editor-cmd=vim 即可实现。
>     如写到启动脚本保存退出，则可执行命令 **source ~/.bash_profile** 来使配置文件立即生效。成功打开文件后一行编写一个忽略的目录或文件即可。保存后会有提示svn:ignore已经修改，此时再执行svn commit提交即可。

### 清空忽略内容

```bash
# 清空svn:ignore的值
svn ps svn:ignore '' ./
property 'svn:ignore' set on '.'
# 删除忽略
svn status --no-ignore
```

### 提交空文件夹

​	提交文件夹 忽略文件夹内容(前提是文件夹未在版本控制内)

```bash
svn propset svn:ignore '*' test
svn ci -m 'adding "test1" and ignore its contents.'
```

### 忽略已提交的文件夹

​	已经创建了文件夹，并加入了版本控制，现在想忽略这个文件夹，但要保持文件夹的内容

```bash
# 导出一个不受版本控制的目录
svn export test1/ ./test1-tmp
Export complete.
# 删除目录
svn rm test1
# 提交
svn ci -m 'delete test1'
# 重名名文件
mv ./test1-tmp/ ./test1
# 将新文件忽略掉
svn ps svn:ignore 'test1' ./
property 'svn:ignore' set on '.'
```

### 忽略多个目录

#### 给属性设置多个值

```bash
# 设置
svn ps svn:ignore "
> d1
> d2
> d3
> " .
property 'svn:ignore' set on '.'
# 查看忽略属性
svn pg svn:ignore
```

#### 通配符

​	属性值也可以使用通配符，但是通配符不可以加在末尾，只能加在前面。

```bash
# 通配符加在末尾会报错
svn ps svn:ignore 'd*' .
'd2' is not under version control
# 通配符加在前面不会报错
svn ps svn:ignore '*2' .
property 'svn:ignore' set on 'test2'
```



