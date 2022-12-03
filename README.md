# learn-git
系统学习Git和GitHub

参考学习：
- [廖雪峰的博客](https://www.liaoxuefeng.com/wiki/896043488029600)
- [GitHub Docs](https://docs.github.com/cn)

## 初始化账户
```powershell
# 初始化账户
git config --global user.name "Brand-Frank"
git config --global user.email "123456789@qq.com"
```

## 初始化版本库
```powershell
git init
```

## 添加文件
```powershell
git add hello-git.txt
```

## 查看状态
```powershell
git status
```

## 编辑文件，查看区别
```powershell
git diff    #需要在git add之前查看，add之后看不到不同之处
```

## 再次提交与查看状态
```powershell
git add .
git status
```

## 查看日志
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

## 退回到上一个版本
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

## 退回到未来的版本
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

## 工作区和暂存区
![工作区和暂存区](images/git-2.jfif)
- `git add`把**文件修改**添加到暂存区；
- `git commit`把暂存区的所有内容提交到当前分支。

## Git只追踪修改，而非文件
实验例程参考[廖雪峰的网站](https://www.liaoxuefeng.com/wiki/896043488029600/897884457270432)

## 查看工作区和版本库里最新版本的区别
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

## 丢弃工作区的修改
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

## 本地仓库与远程仓库建立关联
```powershell
git remote add origin git@github.com:Brand-Frank/learn-git.git    # SSH
# or
git remote add origin https://github.com/Brand-Frank/learn-git.git    #HTTPS
```

## 推送至远程仓库
```powershell
$ git push
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