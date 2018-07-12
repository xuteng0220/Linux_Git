# 安装
1. windows
	Git官网
2. macOS
	xcode
	command line tools(apple developer)
3. Linux
	sudo apt-get install git

## 初始化

```
// 账户信息
$ git config --global user.name "xuteng"
$ git config --global user.email "xuteng0220@gmail.com"


$ git config --global color.ui true  //显示颜色
```


# 基本命令

```
$ pwd
$ cd dirPath
	$ cd ~ 到主目录
	$ cd .. 返回上级目录
$ mkdir fileName
$ open fileName
$ rm fileName
$ mv fileName dirPath  //移动文件到另一个文件夹
$ mv fileName newFileName  //重命名文件
```

>cd /d/xuteng  
绝对路径 cd /d/xuteng/DataScience  
相对路径 cd DataScience  

- 把当前目录变成git可以管理的仓库，该目录下会多一个.git目录（文件夹），默认隐藏，用ls -ah命令查看
$ git init  
	









# Git

## 版本控制系统
版本控制系统能跟踪文本文件（内容）的改动，包括：.txt .html .md 以及程序代码。二进制文件只能记录文本大小的改动，不能跟踪内容

### 版本控制系统结构
1 工作区 working directory（创建、修改文件存储的地方）
2 版本库 
2.1 stage暂存区 （git add后文件暂时存放地）
2.2 master分支以及指向master的指针HEAD （git commit后文件（的修改）所在地方/分支）



## 添加、提交文件
- 添加新文件到git仓库（已有文件修改后提交与之相同）
	- 第一步，把文件添加到仓库  
		$ git add fileName  
		git add把文件（的修改）添加到暂存区
	- 第二步，提交更改  
		$ git commit -m "description"  
		git commit把暂存区的所有内容提交到当前分支
 
```
$ git add fileName    
$ git add fileName1 fileName2
$ git commit -m "add 3 files"
```

## 查看文件内容、仓库状态、提交历史历史
- 查看文件内容
$ cat fileName


- 显示仓库当前的状态，是否有未提交的修改（任何地方使用，随时查看当前状态）  
$ git status


- 查看上一次具体修改的内容  
$ git diff fileName    
	

- 显示历史提交日志(当前git会话的历史提交日志)  
$ git log
$ git log --pretty=oneline （查看历史，显示在一行
）
- 显示每一次提交命令
$ git reflog
	
## 版本回退
- 回退到上一个版本（上一次提交）  
$ git reset --hard HEAD^     
	快速回退是因为git在内部有个指向该版本的指针  
	HEAD表示当前版本，上一个版本就是HEAD^，上上一个版本就是HEAD^^，往上100个版本为HEAD~100
Q：回退到上一版本，再回退一个版本，参数是 HEAD^ 还是 HEAD^^


- 回退（前进）到任意提交过的版本，commit_id  
$ git reset --hard commit_id 
	回到特定

- 记录每一次命令，当退回原版本，又想回到刚才的本版时，可查找commit id
$ git reflog    
	

- 查看工作区文件和版本库里面最新版本的区别
$ git diff HEAD -- fileName
	
## 撤销修改、删除文件
- 撤销修改
	- 修改工作区文件的内容，未git add到暂存区   
	$ git checkout -- fileName  
	将工作区的修改撤销  
	（$ git add到暂存区，未$ git commit。又修改了工作区文件。该命令使回到git add后的暂存区）
	- 修改工作区文件的内容，git add到暂存区，未$ git commit   
	$ git reset HEAD fileName  
	$ git checkout -- fileName   
	命令1把提交到暂存区的修改撤销，回到工作区，命令2把工作区的修改撤销
	- 修改工作区文件的内容，git add到暂存区，git commit到分支  
	$ git reset --hard commit_id  $ git reset HEAD fileName  
	$ git checkout -- fileName 
	对修改$ git commit后，命令1退回到之前某一个版本。再执行命令2、3


- 删除文件

```
$ rm fileName  // 删除工作区文件（版本库不变） 
$ git status  // 查看版本库状态
$ git checkout -- fileName   // rm fileName 误删了工作区的文件，该命令可以从版本库提取（复制）到工作区（版本库中，该文件未删除）
$ git rm fileName  //删除工作区文件，删除版本库文件
$ git commit -m "remove a file"  //将版本库中的文件删除
```








# github
## github注册、准备工作
- 创建SSH key（在用户主目录下。若在主目录下没有.ssh,id_rsa,id_rsa.puh）  
$ ssh-keygen -t rsa -b 4096 -C "xuteng0220@gmail.com"
	
- 将.ssh中的id_rsa.pub（公钥）提交到github  
$ clip < ~/.ssh/id_rsa.pub
	复制id_rsa.pub中的内容(需有clip功能）

## 关联本地与远程仓库
已有本地仓库repoName，在github创建repository，命名repoName（不用勾选readme）

```
$ cd dirPath
$ git init
$ git remote add origin git@gihub.com:xuteng0220/repoName.git
```

## 推送本地仓库到远程
- 首次推送（在需要推送的仓库目录下）
$ git push -u origin master 

```
Q?
git pull --rebase origin master
	github远程仓库原有readme文件，本地无。先执行上述代码，后执行git push -u origin master

git revert commit_id -m "..."
	与git reset ***** 不同
```

- 修改本地仓库后（非首次）推送
$ git add fileName
$ git commit -m "comments"
$ git push origin master 


## 创建远程仓库，克隆到本地
gitHub，创建一个新的仓库，名字叫repoName。勾选readme。选择将要存放该仓库的目录，克隆远程仓库

```
$ cd fileParh
$ git clone git@github.com:xuteng0220/repoName.git
	
$ cd repoName
$ ls
```

## 参与项目
1. fork 复刻github上任意开源的repository，可编辑、修改、开发
2. git clone/pull/push 在本地做开发
3. pull request 在github上将自己的修改提交给repository的创建者

## 远程仓库，多人协作
```
$ git remote  //查看远程库
$ git remote -v  //显示远程库更多详细信息

$ git push origin master   //主分支master需时刻与远程同步
$ git push origin dev    //开发分支也要远程推送，bug和feature分支视情况而定

$ git clone git@git@github.com:xuteng0220/repoName.git  //协作开发者（另一台电脑，或同一台电脑中不同的目录下）从远程克隆分支，得到的是master分支
$ git checkout -b dev origin/dev   //创建本地dev分支
$ git push origin dev    //推送dev分支


```

其他开发者也向同一个远程仓库提交dev分支，修改的内容不同会产生冲突  
1. 将本地的dev与远程的origin/dev进行链接
2. 将他人提交的dev分支pull下来
3. 在本地与自己的dev修改合并后
4. 提交远程

```
$ git branch --set-upstream-to=origin/dev dev   //将本地的dev与远程dev链接
$ git pull


// pull以后，与本地修改冲突，先解决冲突

$ git add ***
$ git commit -m "***"
$ git push origin dev
```















# 分支

## 创建、切换、合并、删除分支
git鼓励使用分支完成某个任务，合并后再删掉分支，这和直接在master分支上工作效果是一样的，但过程更安全

```
$ git checkout -b dev
	// 参数-b表示创建并切换到分支dev
（与以下两条命令等价）
$ git branch dev   
	// 创建分支dev  
$ git checkout dev   
	// 切换分支dev


$ git checkout master  
	//切换回master分支
$ git branch   
	//查看当前所在分支


$ git merge dev   
	//将指定分支合并到当前分支上（首先要$ git checkout 当前分支名）

$ git branch -d dev
	//合并后可以删除分支dev
```



## 解决分支冲突
不同人在不同分支上对同一（名称的）文件进行不同的修改，期望合并分支到master。git无法自动合并，必须首先解决冲突

```
$ git checkout -b feature1  //创建并切换到feature1分支上
	$ git add file1
	$ git commit -m "some comment1"
		// 在feature1分支上，对file1做修改后，添加、提交
$ git checkout master
	$ git add file1
	$ git commit -m "some comment2"
		// 在master分支上，对file1做不同的修改，添加、提交
$ git merge feature1
	// 产生冲突
$ git status  
	// 查看当前（冲突）状态
$ cat file1
	// 查看文件内容，显示冲突部分。
```

### 手动修改成相同文件，解决冲突
打开冲突文件，`<<<<<<<`，`=======`，`>>>>>>>`标记出了不同分支的内容。在此基础上直接修改成想要的最终结果，删除`标记符号`，修改后add，commit

```
$ git add file1
$ git commit -m "fix conflict"
$ git merge future1 // 是否需要这步，可以再试验一下
$ git log --graph --pretty=oneline --abbrev-commit
	// 查看分支合并的情况
$ git branch -d feature1
	// 删除feature1分支
```




### 分支合并，非fast forward模式

```
$ git checkout -b feature2
	$ git add file1
	$ git commit -m "comments"
$ git checkout master
$ git merge --no-ff -m "merge with no-ff" feature2
	以recursive的方式合并分支，因为在Fast forward模式下，删除分支后，会丢掉分支信息。--no-ff参数，以用普通模式合并，合并后的历史有分支，而fast forward合并就看不出来曾经做过合并
$ git log --graph --pretty=oneline --abbrev-commit
```


### 分支策略
master稳定，用来发布版本，不在上面直接修改。修改在dev(develop)上，每个开发参与者又从dev衍生出的分支上修改



### 临时修复bug
1. master上出现bug，需修复
2. 当前在dev分支上工作，有未提交（未git add， git commit）的修改或新内容，git stash可以将它暂存起来
3. 回到master，创建修复分支，修复后合并到master
4. 回到dev分支，git stash pop找回暂存的修改，继续工作

```
$ git status  // 随时查看状态
$ git stash   // 暂存未提交的工作


$ git checkout master
	切换到需要修复的分支上
$ git checkout -b fix_bug 
	创建修复bug分支
$ git add ...
$ git commit -m "..."
$ git checkout master
$ git merge --no-ff -m "bug fixed" fix_bug
$ git branch -d fix_bug

$ git checkout dev
$ git status
$ git stash list  // 查看工作现场

$ git stash apply //恢复工作现场，stash内容不删除
$ git stash drop  //删除stash内容

$ git stash pop  //恢复最近的工作现场，同时删除最近一次stash内容
$ git stash apply stash@{...} // 多次stash，恢复的时候，先用git stash list查看，然后恢复指定的stash，*表示数字，即想要恢复的stash位置（Q：多次stash后要删除stash出现问题？？？）
```

### 强制删除分支
```
$ git checkout -b feature3
$ git add ...
$ git commit -m "..."
$ git checkout dev
$ git branch -D feature3  //删除一个没有被合并过的分支feature3，一般删除（参数 -d）无法完成，需要强制删除(参数 -D)
```




### 整理分支
[rebase](https://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000/0015266568413773c73cdc8b4ab4f9aa9be10ef3078be3f000)



## 标签
标签，是版本库的一个快照，是一个指向某个commit的指针

### 创建标签

```
$ git branch  //查看所有分支
$ git checkout branch_name  //切换到某个分支
$ git tag v2.0   //为给分支上的最新一次commit打上标签，v2.0
$ git tag   //查看所有标签，标签是以字母排列的


$ git log --pretty=online --abbrev-commit   //查看历史commit
$ git tag v1.0 commit_id  //在某个历史commit上打标签，v1.0


$ git show tag_name //查看某个标签的具体信息
$ git tag -a v3.0 -m "..." commit_id    //创建带说明的标签


	$ git tag -s v4.0 -m "signed with code" commit_id
	//创建私钥签名标签，私钥采用PGP前面，需安装GnuPG
```

### 推送、删除变迁
		
```
$ git tag -d v1.0  //删除本地标签（且未推送到远程）
$ git push prigin v1.0  //推送标签
$ git push origin --tags  //推送所有未推送标签


$ git tag -d v2.0  //删除本地标签
$ git push origin :refs/tags/v2.0  //再删除远程标签
```











# 其他

## 忽略特殊文件
$ git status
    显示有untracked files，让它不显示，需在工作区配置.gitignore文件，写入需忽略的文件名
	配置.gitignore文件https://github.com/github/gitignore
	需将.gitignore提交（add,commit）
	
	
## 设置命令别名
```
$ git config --global alias.st status
	$ git st
	$ git status
$ git config --global alias.co checkout
$ git config --global alias.ci commit
$ git config --global alias.br branch
$ git config --global alias.unstage 'reset HEAD'
$ git config --global alias.last 'log -1'
	--global 全局参数，对本电脑所有Git仓库有效。若无--global参数，则别名只对当前仓库有效
```
每个仓库有一个Git配置文件，在.git/config中  

$ cat .git/config  
	查看配置文件。删除别名，删除配置文件中对应的行即可

当前用户的Git配置文件，在主目录下的.gitconfig（隐藏文件）中




## 搭建Git服务器
1.Linux机器，Ubuntu
2.sudo权限的用户

```
$ sudo apt-get install git
	安装git

$ sudo adduser git
	创建一个git用户

把所有公钥（需要登录的用户的id_rsa.pub文件）导入到/home/git/.ssh/authorized_keys文件里，一行一个.

$ sudo git init --bare sample.git
	假定是/srv/sample.git，在/srv目录下输入

$ sudo chown -R git:git sample.git
            把owner改为git

编辑/etc/passwd文件,找到类似下面的一行：
git:x:1001:1001:,,,:/home/git:/bin/bash
改为：
git:x:1001:1001:,,,:/home/git:/usr/bin/git-shell
	禁用shell登录

$ git clone git@server:/srv/sample.git
	克隆远程仓库到本地
```
