# Git 基本认识

## 由来

很多人都知道，Linus在1991年创建了开源的Linux，从此，Linux系统不断发展，已经成为最大的服务器系统软件了。

Linus虽然创建了Linux，但Linux的壮大是靠全世界热心的志愿者参与的，这么多人在世界各地为Linux编写代码，那Linux的代码是如何管理的呢？

事实是，在2002年以前，世界各地的志愿者把源代码文件通过diff的方式发给Linus，然后由Linus本人通过手工方式合并代码！

你也许会想，为什么Linus不把Linux代码放到版本控制系统里呢？不是有CVS、SVN这些免费的版本控制系统吗？因为Linus坚定地反对CVS和SVN，这些集中式的版本控制系统不但速度慢，而且必须联网才能使用。有一些商用的版本控制系统，虽然比CVS、SVN好用，但那是付费的，和Linux的开源精神不符。

不过，到了2002年，Linux系统已经发展了十年了，代码库之大让Linus很难继续通过手工方式管理了，社区的弟兄们也对这种方式表达了强烈不满，于是Linus选择了一个商业的版本控制系统BitKeeper，BitKeeper的东家BitMover公司出于人道主义精神，授权Linux社区免费使用这个版本控制系统。

安定团结的大好局面在2005年就被打破了，原因是Linux社区牛人聚集，不免沾染了一些梁山好汉的江湖习气。开发Samba的Andrew试图破解BitKeeper的协议（这么干的其实也不只他一个），被BitMover公司发现了（监控工作做得不错！），于是BitMover公司怒了，要收回Linux社区的免费使用权。

Linus可以向BitMover公司道个歉，保证以后严格管教弟兄们，嗯，这是不可能的。实际情况是这样的：

Linus花了两周时间自己用C写了一个分布式版本控制系统，这就是Git！一个月之内，Linux系统的源码已经由Git管理了！牛是怎么定义的呢？大家可以体会一下。

Git迅速成为最流行的分布式版本控制系统，尤其是2008年，GitHub网站上线了，它为开源项目免费提供Git存储，无数开源项目开始迁移至GitHub，包括jQuery，PHP，Ruby等等。

历史就是这么偶然，如果不是当年BitMover公司威胁Linux社区，可能现在我们就没有免费而超级好用的Git了。

## 安装

### 在Linux上安装Git

- sudo apt-get install git
- sudo apt-get install git-core
- 从Git官网下载源码，然后解压，依次输入：./config，make，sudo make install 这几个命令安装就好了。

### 在Mac OS X上安装Git

- 新版的系统基本自带
- homebrew安装
- Xcode 安装命令行工具 Command Line Tools

### 在Windows上安装Git

- Git官网直接[下载安装程序](https://git-scm.com/downloads)

## 基本命令

### 本地部分

- 配置 

```
$ git config --global user.name "Your Name"
$ git config --global user.email "email@example.com"
$ git config --global alias.co checkout
```

--global 参数，用了这个参数，表示你这台机器上所有的Git仓库都会使用这个配置，当然也可以对某个仓库指定不同的用户名和Email地址。 



- 创建版本库

```
$ git init
```

- 添加文件

```
$ git add <file>
```

- 提交代码

```
$ git commit -m  <message>
```

- 查看文件修改

```
$ git diff <file>
```

- 查看日志

```
$ git log
```

--graph 参数 可显示分支合并图

- 版本回退

```
$ git reset --hard <commitid>
```

- 查看历史命令

```
$ git reflog
```

- 查看当前状态(修改 新增 删除)

```
$ git status
```

- 放弃当前工作区对某文件的修改(-- 必须有)

```
$ git checkout -- <file>
```

- 删除文件

```
$ git rm file
```


### 分支部分

- 查看当前所有分支和当前分支

```
$ git branch
```

- 创建分支

```
$ git branch <branchname>
```

这个命令不会自动切换

- 切换分支

```
$ git switch <branchname>
```

```
$ git checkout <branchname>
```

不推荐

- 创建并切换新分支

```
$ git switch -c <branchname>
```

不使用-c 不会创建 直接切换

```
$ git checkout -b <branchname>
```

不使用-b 不会创建 这个命令不推荐使用 是比较早的版本命令 语义歧异

- 合并某分支到当前分支

```
$ git merge <branchname>
```

--no-ff 参数显示合并细节 合并后的历史有分支，能看出来曾经做过合并


- 删除分支

```
$ git branch -d <branchname>
```

- 贮藏

```
$ git stash
```

- 抛出贮藏

```
$ git stash pop
```

- 查看贮藏

```
$ git stash list
```

- 删除贮藏

```
$ git stash drop
```

- 恢复某个贮藏

```
$ git stash apply <stash>
```

- 合并某次提交到当前分支

```
$ git cherry-pick <commit>
```

- 合并提交(变基)

```
$ git rebase
```


rebase操作的特点：把分叉的提交历史“整理”成一条直线，看上去更直观。缺点是本地的分叉提交已经被修改过了

- 打tag

```
$ git tag <tagname>
```

<commitid> 从某个提交打tag -m 说明 -a <tagname>

- 删除tag

```
$ git tag  -d <tagname>
```
### 远程部分

- 生成OpenSSH key  (Git支持多种协议，包括https，但ssh协议速度最快)

```
$ ssh-keygen -t rsa -C "youremail@example.com"
```

- 克隆远程库

```
$ git clone <url>
```

- 推送到远端

```
$ git push
```

<remote> <branchname> 指定推送到某个远程分支  不使用则自动推送到跟踪的远程分支

- 从远端更新

```
$ git pull
```

<remote> <branchname> 指定从某个远程分支拉取 不使用则自动从跟踪的远程分支拉取

- 查看远程库

```
$ git remote
```

-v 显示详情


- 设置链接(跟踪)某个远程分支

```
$ git branch --set-upstream-to <branchname> <remote>/<branchname> 
```

- 推送一个本地标签

```
$ git push <remote> <tagname>
```

- 推送所有的tag

```
$ git push <remote> --tags
```


## 工具

sourcetree
- 基本界面
![avatar](https://github.com/purple28flame/picture/blob/master/1.png?raw=true)
- 提交
![avatar](https://github.com/purple28flame/picture/blob/master/2.png?raw=true)
- 推送
![avatar](https://github.com/purple28flame/picture/blob/master/3.png?raw=true)

## 参考

https://www.liaoxuefeng.com/wiki/896043488029600
https://github.com/521xueweihan/git-tips