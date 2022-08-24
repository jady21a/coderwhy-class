# 版本控制
版本控制在软件开发中，可以帮助程序员进行代码的追踪、维护、控制等等一系列的操作
# 历史
- 没有版本控制: 备份的方式来进行管理，再通过 diff 命令来对比两个文件的差异
- CVS（Concurrent Versions System）1985
- SVN（Subversion）2000
- git

cvs 和 svn 都是集中式版本控制
git 是分布式的版本控制

# 集中和分布
- 集中式版本控制系统（Centralized Version Control Systems，简称 CVCS）
一个服务器集中管理，保存所有文件的修订版本；
其他人从这个服务器提交和下载资源
缺点: 
中央服务器不能出现故障
- 布式版本控制系统（Distributed Version Control System，简称 DVCS）
客户端并不只提取最新版本的文件快照，而是把代码仓库完整地镜像下来，包括完整的历史记录；

# git
https://git-scm.com/downloads

## Bash – CMD – GUI 区别
- Bash 就是一个 shell
是 Windows 下的命令行工具，可以执行 Linux 命令；
基于 CMD ，在 CMD 的基础上增添一些新的命令与功能；
- Git CMD
命令行提示符（CMD）是 Windows 操作系统上的命令行解释程序；
- Git GUI
图形用户界面来运行 git 命令；

## git 配置
用户配置
git config --global user. name "jady"
git config --global user. email "xyzjady21@outlook. com"

设置
git config
git config  --system 系统配置文件 (系统里可以有多个用户)
git config --global 只针对当前用户, 所有的仓库生效
git config --local 针对该仓库, 默认使用

◼ 检测当前的配置信息：git config --list
退出信息界面:  q

git config user.name
![[Pasted image 20220824001934.png]]

## 命令行起别名
![[Pasted image 20220824002147.png]]

## 获取 git 仓库
1. 自己初始化  
	git init
	git add .
	git cm -m " "
2. 从远程仓库 clone
	git clone xxxxxxxx (xxxx 为仓库地址)

## 文件的状态:
查看状态: git status
		git status -s = git status --short

- 未跟踪 (untracked):  没有add
- 已跟踪 (tracked): add 之后
	- staged 暂缓区状态 (add 后没有 commit)
	- unmodified (add 后 commit, 没有修改内容了)
	- modified (有修改内容)

## git add  cm -m
git add aaa. js  (添加 aa. js 到暂缓区)
git add . (全部添加到暂缓区)

git commit -m " info"
简写
git commit -a -m "info" = git cm -a -m "info"

## 提交日志
git log
git log --pretty=oneline
git log --pretty=oneline --graph  (分支以图表形式展示)

## 版本回退
校验和  --> commit id (版本 id)
![[Pasted image 20220824210235.png]]
- 回退到上一个版本: git reset --hard HEAD^
- 回退 10 个版本: git reset --hard HEAD~10
- 指定某一个 commit id: git reset --hard 4fe73cc2

## ignore  
[github/gitignore: A collection of useful .gitignore templates](https://github.com/github/gitignore)
. gitignore 的文件, 列出需要忽略不提交的文件 ![[Pasted image 20220824224541.png]]
如: 本地环境变量文件, 日志文件, 编辑器自动生成的文件；



# git 远程
## ssh
生产公钥和私钥
ssh-keygen -t ed25519 -C “your email" 
ssh-keygen -t rsa -b 2048 -C “your email"

## 远程仓库
查看
git remote 
git remote –v    ( v 是 verbose 的缩写 (冗长的))
![[Pasted image 20220824211153.png]]

添加远程地址 ?
git remote add \<name> xxxxx (地址)
如: git remote add test git@github. com: jady21a/test-git. git

重命名远程地址:  git remote rename test test2
移除远程地址: git remote remove test2



## 本地的跟踪分支 (上游分支)
- simple  (默认): 本地 push 分支名需与远程分支名相同
- upstream: 设置上游分支, 本地 push 到指定的远程分支名
- current
- tracking
![[Pasted image 20220824144358.png]]

## 没有共同分支的两个仓库连接后
不能 pull 的原因
1. 不能 fetch : 设置跟踪
	git branch --set-upstream-to=origin/master
2. 不能 merge: 设置允许不相关历史合并
	git merge --allow-unrelated-history

## 远程分支操作

1. git clone xxxxxx
2. 有本地有远程 (分支名不一样)
	本地 git init
		git remote add origin xxxx
	获取远程内容
- git checkout main  
	git pull
-  git branch --set-upstream-to=origin/main
	git merge --allow-unrelated-histories
	git pull

使用 dev 远程分支 
git checkout develop
删除
git push origin --delete dev


![[Pasted image 20220824133741.png]]

# 杂知识
## 开源协议
![[Pasted image 20220824215949.png]]
## git tag
- 轻量标签（lightweight）
	git tag v1.0.0
- 附注标签（annotated）
	git tag -a v1.1.0 -m "info"

◼ 默认情况下，git push 命令并不会传送标签到远程仓库服务器上。需要手动推送
git push origin v1.0.0
git push origin --tags

删除 tag
git tag -d v1.0.0
git push origin --delete v1.1.0

检出 tag
git checkout v1.1.0

## git flow (git 工作流)
![[Pasted image 20220824221134.png]]
![[Pasted image 20220824221143.png]]

## merge 和 rebase
![[Pasted image 20220824221426.png]]
merge
$ git checkout master 
$ git merge experiment
![[Pasted image 20220824221447.png]]
rebase 改变当前分支的 base
git checkout experiment 
git rebase master
![[Pasted image 20220824222724.png]]
永远不要在主分支上使用 rebase
会造成大量的提交历史在 main 分支中不同；
多人开发时，其他人依然在原来的 main 中，对于提交历史来说会有很大的变化；


# git 分支
创建 test 分支
	git branch test
切换分支
	git checkout test
	git checkout master
创建分支并切换
	git checkout -b test
查看分支
	git branch # 查看当前所有的分支 
	git branch –v # 同时查看最后一次提交 
	git branch --merged # 查看所有合并到当前分支的分支 
	git branch --no-merged # 查看所有没有合并到当前分支的分支

# 命令速查表
![[Pasted image 20220824223009.png]]

