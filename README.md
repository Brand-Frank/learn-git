# learn-git
系统学习Git和GitHub

参考学习：
- [廖雪峰的博客](https://www.liaoxuefeng.com/wiki/896043488029600)
- [GitHub Docs](https://docs.github.com/cn)

- [Git简介](#Git简介)
  - [初始化账户](#初始化账户)
  - [初始化版本库](#初始化版本库)
  - [添加文件](#添加文件)
  - [查看状态](#查看状态)
  - [编辑文件，查看区别](#编辑文件，查看区别)
  - [再次提交与查看状态](#再次提交与查看状态)
  - [查看日志](#查看日志)

- [Git本地仓库管理](#Git本地仓库管理)
  - [退回到上一个版本](#退回到上一个版本)
  - [退回到未来的版本](#退回到未来的版本)
  - [工作区和暂存区](#工作区和暂存区)
  - [Git只追踪修改，而非文件](#Git只追踪修改，而非文件)
  - [查看工作区和版本库里最新版本的区别](#查看工作区和版本库里最新版本的区别)
  - [丢弃工作区的修改](#丢弃工作区的修改)
- [远程仓库](#远程仓库)
  - [本地仓库与远程仓库建立关联](#本地仓库与远程仓库建立关联)
  - [推送至远程仓库](#推送至远程仓库)
  - [丢弃工作区的修改](#丢弃工作区的修改)
  - [删除与远程仓库的绑定关系](#删除与远程仓库的绑定关系)
  - [从远程仓库克隆到本地](#从远程仓库克隆到本地)
- [分支管理](#分支管理)
  - [创建与合并分支](#创建与合并分支)
    - [创建dev分支](#创建dev分支)
  - [推送至远程仓库](#推送至远程仓库)
  - [丢弃工作区的修改](#丢弃工作区的修改)
  - [删除与远程仓库的绑定关系](#删除与远程仓库的绑定关系)
  - [从远程仓库克隆到本地](#从远程仓库克隆到本地)



## Git简介
### 初始化账户
```powershell
# 初始化账户
git config --global user.name "Brand-Frank"
git config --global user.email "123456789@qq.com"
```

### 初始化版本库
```powershell
git init
```

### 添加文件
```powershell
git add hello-git.txt
```

### 查看状态
```powershell
git status
```

### 编辑文件，查看区别
```powershell
git diff    #需要在git add之前查看，add之后看不到不同之处
```

### 再次提交与查看状态
```powershell
git add .
git status
```

### 查看日志
```powershell
git log
```
```powershell
commit 7c4bd2b3f63e63990b657f7ce67cd035c40e2dc5 (HEAD -> main)
Author: Brand-Frank <3069584010@qq.com>
Date:   Sat Dec 3 19:51:06 2022 +0800

    append GPL

commit f1ef8f3e4b2d11b2ca8cf1f65440635f02e38a2e
Author: Brand-Frank <3069584010@qq.com>
Date:   Sat Dec 3 19:48:04 2022 +0800

    add distributed

commit 06b98edccbf6c6115efcc86857a7bfc94f86b53f
Author: Brand-Frank <3069584010@qq.com>
Date:   Sat Dec 3 19:38:56 2022 +0800

    add a file.

commit d7b220918c360dc4f044532911498ef8c02f7b34
Author: Brand-Frank <3069584010@qq.com>
Date:   Sat Dec 3 19:36:41 2022 +0800

    wrote a hello-git file.

commit 30d25aaf35c014c4b4e309f3dbd2c3043bc6845b (origin/main, origin/HEAD)
Author: inTree <54088180+Brand-Frank@users.noreply.github.com>
Date:   Sat Dec 3 19:07:15 2022 +0800

    Update README.md

commit cd9255a9d6041daf8979aa228e4fb846e0e97baf
Author: inTree <54088180+Brand-Frank@users.noreply.github.com>
Date:   Sat Dec 3 19:05:08 2022 +0800

    Initial commit
```

- 简化方式查看日志
```powershell
git log --pretty=oneline
```
输出情况
```powershell
7c4bd2b3f63e63990b657f7ce67cd035c40e2dc5 (HEAD -> main) append GPL    # HEAD, will be delete
f1ef8f3e4b2d11b2ca8cf1f65440635f02e38a2e add distributed
06b98edccbf6c6115efcc86857a7bfc94f86b53f add a file.
d7b220918c360dc4f044532911498ef8c02f7b34 wrote a hello-git file.
30d25aaf35c014c4b4e309f3dbd2c3043bc6845b (origin/main, origin/HEAD) Update README.md
cd9255a9d6041daf8979aa228e4fb846e0e97baf Initial commit
```
- `7c4bd2b3f63e63990b657f7ce67cd035c40e2dc5`为`commit id`（版本号），是由SHA1计算出来的一个非常大的数字，十六进制表示

## Git本地仓库管理
### 退回到上一个版本
- Git中，用`HEAD`来表示当前版本，也就是最新提交的`7c4bd2b3f63e63990b657f7ce67cd035c40e2dc5`，上一个版本是`HEAD^`，再上一个版本是`HEAD^^`，较多`^`时，写作`HEAD~100`，往前数的第一百个版本。

```powershell
git reset --hard HEAD^    #往回退回上一个版本
```
用`git log --hard HEAD^`查看一下日志情况
```powershell
cfd4505bb3ee566309407086f8d4b52b848e6d30 (HEAD -> main) Retry again
f1ef8f3e4b2d11b2ca8cf1f65440635f02e38a2e add distrbuted
06b98edccbf6c6115efcc86857a7bfc94f86b53f add a file.
d7b220918c360dc4f044532911498ef8c02f7b34 wrote a hello-git file.
30d25aaf35c014c4b4e309f3dbd2c3043bc6845b (origin/main, origin/HEAD) Update README.md
cd9255a9d6041daf8979aa228e4fb846e0e97baf Initial commit
```

- 只要这个命令行窗口还没有被关掉，就可以找到下一个的`commit id`，指定回到未来的某个版本
```powershell
git reset --hard 7c4bd    #不用写全commit id，git会自动寻找
```

<p style="text-align:center; color:purple; padding:1px; border:1px solid black">Note: git 工作原理</p>
<img src="images/git-1.png" alt="git-1.png" style="width:auto; border:1px solid black">

### 退回到未来的版本
在Git中，总是有后悔药可以吃的。当你用`git reset --hard HEAD^`回退到<em><strong>add distributed</strong></em>版本时，再想恢复到**append GPL**，就必须找到**append GPL**的`commit id`。Git提供了一个命令`git reflog`用来**记录你的每一次命令**：
```powershell
PS E:\CSB\Git\learn-git> git reflog
0dc07a4 (HEAD -> main) HEAD@{0}: commit: hello here
d7b2209 HEAD@{1}: reset: moving to HEAD^^
f1ef8f3 HEAD@{2}: reset: moving to HEAD^
7c4bd2b HEAD@{3}: reset: moving to 7c4bd
cfd4505 HEAD@{4}: reset: moving to HEAD^
422de07 HEAD@{5}: commit: add a note
cfd4505 HEAD@{6}: commit: Retry again
f1ef8f3 HEAD@{7}: reset: moving to HEAD^
7c4bd2b HEAD@{8}: commit: append GPL
f1ef8f3 HEAD@{9}: commit: add distributed
06b98ed HEAD@{10}: commit: add a file.
d7b2209 HEAD@{11}: commit: wrote a hello-git file.
30d25aa (origin/main, origin/HEAD) HEAD@{12}: clone: from https://github.com/Brand-Frank/learn-git.git
```

### 工作区和暂存区
![工作区和暂存区](images/git-2.jfif)
- `git add`把**文件修改**添加到暂存区；
- `git commit`把暂存区的所有内容提交到当前分支。

### Git只追踪修改，而非文件
实验例程参考[廖雪峰的网站](https://www.liaoxuefeng.com/wiki/896043488029600/897884457270432)

### 查看工作区和版本库里最新版本的区别
```powershell
git diff HEAD -- hello-git.txt
```
输出内容：
```powershell
PS E:\CSB\Git\learn-git> git diff HEAD -- hello-git.txt
diff --git a/hello-git.txt b/hello-git.txt
index 56b2aa4..053de74 100644
--- a/hello-git.txt
+++ b/hello-git.txt
@@ -2,4 +2,5 @@ Git is a version control system.
 Git is free software.
 Git has a mutable index called stage.

-Git tracks changes, but not files.
\ No newline at end of file
+Git tracks changes, but not files.
+Git tracks changes of files.
\ No newline at end of file
PS E:\CSB\Git\learn-git> git add --all
PS E:\CSB\Git\learn-git> git commit -m "OK"
```

### 丢弃工作区的修改
```powershell
git checkout -- hello-git.txt    #把hello-git文件在工作区的修改全部撤销，而且此时工作区的修改没有添加到暂存区(add)
```
- 一种是`hello-git.txt`*自修改后还没有被放到暂存区*，现在，撤销修改就回到**和版本库一模一样的状态**；
- 一种是`hello-git.txt`*已经添加到暂存区后，又作了修改*，现在，撤销修改就回到**添加到暂存区后的状态**。

- 已经`git add`到暂存区了：`My stupid boss still prefers SVN.`, `git add hello-git.txt`
```powershell
git reset HEAD hello-git.txt    #git reset可以回退版本，也可以把暂存区的修改回退到工作区
git checkout -- hello-git.txt    #丢弃工作区的修改

# Note 廖老师的可能有点问题，实验时没有复现出来，尝试使用下面的命令，成功！
git reset --hard HEAD^
```

## 远程仓库
### 本地仓库与远程仓库建立关联
```powershell
git remote add origin git@github.com:Brand-Frank/learn-git.git    # SSH
# or
git remote add origin https://github.com/Brand-Frank/learn-git.git    #HTTPS
```

### 推送至远程仓库
```powershell
$ git push
```
输出情况：
```powershell
Enumerating objects: 41, done.
Counting objects: 100% (41/41), done.
Delta compression using up to 16 threads
Compressing objects: 100% (35/35), done.
Writing objects: 100% (39/39), 5.69 KiB | 1.90 MiB/s, done.
Total 39 (delta 17), reused 0 (delta 0), pack-reused 0
remote: Resolving deltas: 100% (17/17), done.
To https://github.com/Brand-Frank/learn-git.git
   30d25aa..cea6148  main -> main
```
- 增加两张本地链接的图片
```powershell
$ git push origin main
```
输出情况：
```powershell
Enumerating objects: 10, done.
Counting objects: 100% (10/10), done.
Delta compression using up to 16 threads
Compressing objects: 100% (8/8), done.
Writing objects: 100% (8/8), 76.02 KiB | 25.34 MiB/s, done.
Total 8 (delta 3), reused 0 (delta 0), pack-reused 0
remote: Resolving deltas: 100% (3/3), completed with 2 local objects.
To https://github.com/Brand-Frank/learn-git.git
   cea6148..b7d80a6  main -> main
```

### 删除与远程仓库的绑定关系
> 如果添加的时候远程仓库地址写错了，或者就是想删除远程仓库们可以用`git remote rm <name>`命令，使用前，建议先用`git remote -v`查看远程仓库信息：
> - <p style="font-size:1.2rem; background-color:yellow">注意：</p>这里的删除其实是接触本地和远程的绑定关系，并不是物理上删除远程库。远程库本身并没有变动。要真正删除远程库，需要登陆到GitHub，在后台页面找到删除按钮再删除。

```powershell
git remote -v
###
origin  https://github.com/Brand-Frank/learn-git.git (fetch)
origin  https://github.com/Brand-Frank/learn-git.git (push)
```

### 从远程仓库克隆到本地
```powershell
git clone https://github.com/Brand-Frank/learn-git.git
```

## 分支管理

### 创建与合并分支
[分支详细讲解](https://www.liaoxuefeng.com/wiki/896043488029600/900003767775424)
- **这里的`master`应当为`main`，但是为了与这里的图片匹配，都用`master`来表示了，但是`master`应为种族歧视问题已经在2020年开始弃用了，创建的默认分支均为`main`分支**
> 截止到目前，只有一条时间线，在Git里，这个分支叫主分支，即`master`分支。`HEAD`严格来说不是指向提交，而是指向`master`，`master`才是指向提交的，所以，`HEAD`指向的就是**当前分支**。

一开始的时候，`master`分支是一条线，Git用`master`指向最新的提交，再用`HEAD`指向`master`，就能确定当前分支，以及当前分支的提交点：

![git-br-initial](images/git-br-initial.png)

每次提交，`master`分支都会向前移动一步，这样，随着你不断提交，`master`分支的线也越来越长。
**当我们创建新的分支，例如`dev`时，Git新建了一个指针叫`dev`，指向`master`相同的提交，再把`HEAD`指向`dev`，就表示当前分支在`dev`上**：

![git-br-create](images/git-br-create.png)

Git创建一个分支很快，因为除了**增加一个`dev`指针**，**改改`HEAD`的指向**，**工作区的文件都没有任何变化**！

不过，从现在开始，对工作区的修改和提交就是针对`dev`分支了，比如新提交一次后，`dev`指针往前移动一步，而`master`指针不变：
![git-br-dev-fd](images/git-br-dev-fd.png)

假如我们在dev上的工作完成了，就可以把`dev`合并到`master`上。Git怎么合并呢？最简单的方法，就是直接把`master`指向`dev`的当前提交，就完成了合并：

![git-br-ff-merge](images/git-br-ff-merge.png)

所以Git合并分支也很快！就改改指针，工作区内容也不变！

合并完分支后，甚至可以删除`dev`分支。删除dev分支就是把dev指针给删掉，删掉后，我们就剩下了一条`master`分支：

![git-br-rm](images/git-br-rm.png)

#### 创建与切换dev分支
```powershell
## method-1
git branch dev    # 创建dev分支
git checkout dev    # 切换到dev分支
###
Switched to branch 'dev'
M       README.md

## method-2
git checkout -b dev    #创建并切换到dev分支
#Note 这里不能复现廖老师的实验，所以建议用上面的方法创建并切换至dev分支
```

#### 列出所有分支
```powershell
$ git branch
###
  dev
* mai
```

#### 在分支上做出修改并提交
```powershell
$ echo "Create a new branch is quick." >> hello-git.txt
$ git add --all
$ git commit -m "branch test"
```
#### 切换回主分支(main)
```powershell
git checkout main
```
切换回master分支后，再查看一个readme.txt文件，刚才添加的内容不见了！因为那个提交是在dev分支上，而master分支此刻的提交点并没有变:
![git-br-on-master](images/git-br-on-master.png)

#### 合并分支(dev)到主分支(main)
```powershell
git merge dev    # 合并指定分支到当前分支
```
合并后，再查看`readme.txt`的内容，就可以看到，和`dev`分支的最新提交是完全一样的。注意到上面的*Fast-forward*信息，Git告诉我们，这次合并是“**快进模式**”，也就是直接把`master`指向`dev`的当前提交，所以合并速度非常快。

#### 删除分支(dev)



### 解决冲突
### 分支管理策略
### Bug分支
### Feature分支
### 多人协作
### Rebase



### 




## 标签管理