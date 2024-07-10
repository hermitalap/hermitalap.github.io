# Git

# Git 是一个分布式版本控制系统.
文本，脚本，以及各种基于文本信息的文件可被Git管理

各软件私有格式、二进制文件、媒体不可被Git管理


## 安装
官方下载地址，[Git](https://git-scm.com/downloads)

### GUI管理器
[GitHub Desktop](https://desktop.github.com/)
[Sourcetree](https://www.sourcetreeapp.com/)

## 基本使用
### 基本配置
设置个人信息，用于将修改与人对应
```git
$ git config --global user.name "username"
$ git config --global user.email "email@example.com"
```

### (init）创建版本库 Repository
首先cd到你要管理的文件夹
然后创建
```shell
git init
# Initialized empty Git repository in somefoloers/.git/

# 提示：使用 'master' 作为初始分支的名称。这个默认分支名称可能会更改。要在新仓库中
# 提示：配置使用初始分支名，并消除这条警告，请执行：
# 提示：
# 提示：  git config --global init.defaultBranch <名称>
# 提示：
# 提示：除了 'master' 之外，通常选定的名字有 'main'、'trunk' 和 'development'。
# 提示：可以通过以下命令重命名刚创建的分支：
# 提示：
# 提示：  git branch -m <name>
```
git 创建的管理库文件 `.git` 是被隐藏起来的

### (add）添加文件管理

建立一个新的 1.py 文件:
```bash
$ touch first.py
```

现在 `first.py` 并没有被放入版本库中 (unstaged), 所以我们要使用 `add` 把它添加进版本库 (staged):

```shell
$ git add first.py

# 再次查看状态 status
$ git status
位于分支 master  
  
尚无提交  
  
要提交的变更：  
（使用 "git rm --cached <文件>..." 以取消暂存）  
新文件： first.py
```

如果想一次性添加文件夹中所有未被添加的文件, 可以使用这个:

```shell
$ git add .
```

###  (commit）提交改变

我们已经添加好了 `first.py` 文件, 最后一步就是提交这次的改变, 并在 `-m` 自定义这次改变的信息:

```shell
$ git commit -m "create first.py"

# 输出
[master（根提交） d722a66] create first.py  
1 file changed, 0 insertions(+), 0 deletions(-)  
create mode 100644 first.py

$ git commit -am "change 3 in dev" # "-am": add 所有改变 并直接 commit
```

### (log）修改记录
查看

```shell
$ git log

# 输出
commit d722a6689063eebd44a4584c07c7bf613520b5d5 (HEAD -> master)  
Author: xxx <xxx@126.com>  
Date: Mon Aug 30 21:38:36 2021 +0800  

create first.py

$ git log --oneline # "--oneline": 每个 commit 内容显示在一行,更简洁，不显示时间

9aeb5f1 (HEAD -> master) create second.py  
d722a66 create first.py
```

### (diff）查看 unstaged

如果想要查看这次还没 `add` (unstaged) 的修改部分 和上个已经 `commit` 的文件有何不同, 我们将使用 `$ git diff`:

```shell
$ git diff

# 输出
diff --git a/first.py b/first.py  
index e69de29..1337a53 100644  
--- a/first.py  
+++ b/first.py  
@@ -0,0 +1 @@  
+a = 1
```
注意这里不会显示你还没有追踪的文件，也就是还没有add的文件修改并不会被显示

### (diff --cached）查看 staged 

如果你已经 `add` 了这次修改, 文件变成了 “可提交状态 (staged)”, 我们可以在 `diff` 中添加参数 `--cached` 来查看修改:

```shell
$ git add .   # add 全部修改文件
$ git diff --cached

# 输出
diff --git a/1.py b/1.py
index 1337a53..ff7c36c 100644
--- a/1.py
+++ b/1.py
@@ -1 +1,2 @@
-a = 1
+a = 2
+b = 1
```

###  (diff HEAD）查看 staged & unstaged
显示所有的修改，不管是否为staged（已add）或unstaged（未add）

目前 `a = 2` 和 `b = 1` 已被 `add`, `c = b` 是新的修改, 还没被 `add`.

```shell
# 对比三种不同 diff 形式
$ git diff HEAD     # staged & unstaged

@@ -1 +1,3 @@
-a = 1  # 已 staged
+a = 2  # 已 staged
+b = 1  # 已 staged
+c = b  # 还没 add 去 stage (unstaged)
-----------------------
$ git diff          # unstaged

@@ -1,2 +1,3 @@
 a = 2  # 注: 前面没有 +
 b = 1  # 注: 前面没有 +
+c = b  # 还没 add 去 stage (unstaged)
-----------------------
$ git diff --cached # staged

@@ -1 +1,2 @@
-a = 1  # 已 staged
+a = 2  # 已 staged
+b = 1  # 已 staged
```

### (commit --amend）修改已 commit 的版本

有时候我们总会忘了什么, 比如已经提交了 `commit` 却发现在这个 `commit` 中忘了附上另一个文件. 接下来我们模拟这种情况. 上节内容中, 我们最后一个 `commit` 是 `change 2`, 我们将要添加另外一个文件, 将这个修改也 `commit` 进 `change 2`. 所以我们复制 `1.py` 这个文件, 改名为 `2.py`. 并把 `2.py` 变成 `staged`, 然后使用 `--amend` 将这次改变合并到之前的 `change 2` 中.

```shell
$ git add 2.py
$ git commit --amend --no-edit   # "--no-edit": 不编辑, 直接合并到上一个 commit
$ git log --oneline    # "--oneline": 每个 commit 内容显示在一行

# 输出
904e1ba change 2    # 合并过的 change 2
c6762a1 change 1
13be9a7 create 1.py
```

### (reset）回到unstaged状态

有时我们添加 `add` 了修改, 但是又后悔, 并想补充一些内容再 `add`. 这时, 我们有一种方式可以回到 `add` 之前. 比如在 `1.py` 文件中添加这一行:
```
d = 3
```

然后 `add` 去 `staged` 再返回到 `add` 之前:

```shell
$ git add 1.py
$ git status -s # "-s": status 的缩写模式
# 输出
M  1.py     # staged，绿色M
-----------------------
$ git reset 1.py
# 输出
重置后取消暂存的变更：  
M 1.py
-----------------------
$ git status -s
# 输出
 M 1.py     # unstaged，红色M
```

### (reset --hard xxxxxx）回到 commit 之前

在穿梭到过去的 `commit` 之前, 我们必须了解 git 是如何一步一步累加更改的. 我们截取网上的一些图片

![](Pasted%20image%2020210903164629.png " ")

![](Pasted%20image%2020210903164635.png " ")

![](Pasted%20image%2020210903164641.png " ")

![](Pasted%20image%2020210903164647.png " ")

每个 `commit` 都有自己的 `id` 数字号, `HEAD` 是一个指针, 指引当前的状态是在哪个 `commit`. 最近的一次 `commit` 在最右边, 我们如果要回到过去, 就是让 `HEAD` 回到过去并 `reset` 此时的 `HEAD` 到过去的位置.

```shell
# 不管我们之前有没有做了一些 add 工作, 这一步让我们回到 上一次的 commit
$ git reset --hard HEAD    
# 输出
HEAD is now at 904e1ba change 2
-----------------------
# 看看所有的log
$ git log --oneline
# 输出
904e1ba change 2
c6762a1 change 1
13be9a7 create 1.py
-----------------------
# 回到 c6762a1 change 1
# 方式1: "HEAD^"
$ git reset --hard HEAD^  

# 方式2: "commit id"
$ git reset --hard c6762a1
-----------------------
# 看看现在的 log
$ git log --oneline
# 输出
c6762a1 change 1
13be9a7 create 1.py
```

此时回到了`change 1`, 在此之后的修改都消失了，我们可以查看 `$ git reflog` 里面最近做的所有 `HEAD` 的改动, 并选择想要回到的 `commit id`:

```shell
$ git reflog
# 输出
c6762a1 HEAD@{0}: reset: moving to c6762a1
904e1ba HEAD@{1}: commit (amend): change 2
0107760 HEAD@{2}: commit: change 2
c6762a1 HEAD@{3}: commit: change 1
13be9a7 HEAD@{4}: commit (initial): create 1.py
```

重复 `reset` 步骤就能回到 `commit (amend): change 2` (id=904e1ba)这一步了:

```shell
$ git reset --hard 904e1ba
$ git log --oneline
# 输出
904e1ba change 2
c6762a1 change 1
13be9a7 create 1.py
```

我们又再次回到了 `change 2`.

### (checkout）改写文件 

其实 `checkout` 最主要的用途并不是让单个文件回到过去, 我们之后会继续讲 `checkout` 在分支 `branch` 中的应用, 这一节主要讲 `checkout` 让文件回到过去.

我们现在的版本库中有两个文件:

```
- gitTUT
    - 1.py
    - 2.py
```

我们仅仅要对 `1.py` 进行回到过去操作, 回到 `c6762a1 change 1` 这一个 `commit`. 使用 `checkout` + id `c6762a1` + `--` + 文件目录 `1.py`, 我们就能将 `1.py` 的指针 `HEAD` 放在这个时刻 `c6762a1`:

```shell
$ git log --oneline
# 输出
904e1ba change 2
c6762a1 change 1
13be9a7 create 1.py
---------------------
$ git checkout c6762a1 -- 1.py
```

这时 `1.py` 文件的内容就变成了:
```
a = 1
```

我们在 `1.py` 加上一行内容 `# I went back to change 1` 然后 `add` 并 `commit` `1.py`:

```shell
$ git add 1.py
$ git commit -m "back to change 1 and add comment for 1.py"
$ git log --oneline

# 输出
47f167e back to change 1 and add comment for 1.py
904e1ba change 2
c6762a1 change 1
13be9a7 create 1.py
```

可以看出, 不像 `reset` 时那样, 我们的 `change 2` 并没有消失, 但是 `1.py` 却已经回去了过去, 并改写了未来.

## 分支管理
### (branch dev）使用branch创建分支
我们建立另一个分支 `dev`, 并查看所有分支:

```shell
$ git branch dev    # 建立 dev 分支
$ git branch        # 查看当前分支

# 输出
  dev       
* master    # * 代表了当前的 HEAD 所在的分支
```

当我们想把 `HEAD` 切换去 `dev` 分支的时候, 我们可以用到上次说的 `checkout`:

```shell
$ git checkout dev

# 输出
Switched to branch 'dev'
```

### (log --oneline --graph）使用graph观看分支
```shell
$ git branch

# 输出
* dev       # 这时 HEAD 已经被切换至 dev 分支
  master
  
$ git log --oneline --graph

# 输出
* 9f3367b (HEAD -> dev) create dev branch
* 9aeb5f1 (master) create second.py
* d722a66 create first.py
```
### (checkout -b）直接创建并切换到新建的分支
使用 `checkout -b` + 分支名, 就能直接创建和切换到新建的分支:

```shell
$ git checkout -b  dev

# 输出
Switched to a new branch 'dev'
--------------------------
$ git branch

# 输出
* dev       # 这时 HEAD 已经被切换至 dev 分支
  master
```
### (merge）将 dev 的修改推送到 master
们 `dev` 中的修改推送到 `master` 中，首先要切换到 `master`, 再将 `dev` 推送过来.

```shell
$ git checkout master   # 切换至 master 才能把其他分支合并过来

$ git merge dev         # 将 dev merge 到 master 中
$ git log --oneline --graph

# 输出
* f9584f8 change 3 in dev
* 47f167e back to change 1 and add comment for 1.py
* 904e1ba change 2
* c6762a1 change 1
* 13be9a7 create 1.py
```

要注意的是, 如果直接 `git merge dev`, git 会采用默认的 `Fast forward` 格式进行 `merge`, 这样 `merge` 的这次操作不会有 `commit` 信息. `log` 中也不会有分支的图案. 我们可以采取 `--no-ff` 这种方式保留 `merge` 的 `commit` 信息.

```shell
$ git merge --no-ff -m "keep merge info" dev         # 保留 merge 信息
$ git log --oneline --graph

# 输出
*   c60668f keep merge info
|\  
| * f9584f8 change 3 in dev         # 这里就能看出, 我们建立过一个分支
|/  
* 47f167e back to change 1 and add comment for 1.py
* 904e1ba change 2
* c6762a1 change 1
* 13be9a7 create 1.py
```
### (commit）解决冲突
如果对于同一个文件，master和dev进行了不同的修改，也就是说在 `master` 和 `dev` 上的版本是不同的，此时`merge` 就会有冲突，提示为
```shell
Auto-merging 1.py CONFLICT (content): Merge conflict in 1.py Automatic merge failed; fix conflicts and then commit the result.
```
此时分支其实已经合并了，但是存在冲突的文件会被git自动进行标注，以方便我们解决冲突，打开1.py可以看到
```shell
a = 1
# I went back to change 1
<<<<<<< HEAD
# edited in master
=======
# edited in dev
>>>>>>> dev
```

我们只需要手动处理被标记出来的冲突行即可，可以这么进行理解，对于该冲突文件，git进行标记，产生了一个不同于master和dev的第三个版本的文件，此时我们需要手动将该文件编辑为合适的正确的第三版本文件，并记得解决完冲突后进行commit，将其确定为主分支的唯一版本。
然后再 `commit` 现在的文件, 冲突就解决啦.

```shell
$ git commit -am "solve conflict"
```

再来看看 `master` 的 `log`:

```shell
$ git log --oneline --graph

# 输出
*   7810065 solve conflict
|\  
| * f7d2e3a change 3 in dev
* | 3d7796e change 4 in master
|/  
* 47f167e back to change 1 and add comment for 1.py
* 904e1ba change 2
* c6762a1 change 1
* 13be9a7 create 1.py
```
可以看到，第一次merge时，并没有产生版本号，也就是出现冲突后产生了一个“待解决”过渡版本，随后我们解决完冲突后进行commit才可以产生正确的唯一分支。


### (rebase）变基

同样是合并， `rebase` 的做法和 `merge` 不一样.

假设共享的 branch 是 `branch B`, 而我在 `branch A` 上工作, 有一天我发现`branch B`已经有一些小更新, 我也想试试我的程序和这些小更新兼不兼容, 但我并不想直接合并我的未完成版本到 `branch A`上, 这时就可以用 `rebase` 来补充我的分支`branch B`的内容. 补充完以后, 和后面那张图的 `merge` 不同, 我还是继续在 `C3` 上工作, 不过此时的 `C3` 的本质却不一样了, 因为吸收了那些小更新. 所以我们用 `C3'` 来代替.

![](Pasted%20image%2020210901175904.png "原分支")

![](Pasted%20image%2020210901175908.png "将C3变为变基状态")

![](Pasted%20image%2020210901175912.png "将C3的基变为C4")

![](Pasted%20image%2020210901175916.png "以C4为新的基，原分支A上的修改被合并")

可以看出 `rebase` 改变了 `C3` 的属性, `C3` 已经不是从 `C1` 衍生而来的了. 这一点和 `merge` 不一样. `merge` 在合并的时候创建了一个新的 `C5` `commit`. 这一点不同, 使得在共享分支中使用 `rebase` 变得危险. 如果是共享分支的历史被改写. 别人之前共享内容的 `commit` 就被你的 `rebase` 修改掉了.

![](Pasted%20image%2020210901175926.png "改写历史")

此外，需要注意的是， **!!! 只能在你自己的分支中使用 rebase, 和别人共享的部分是不能用的 !!!**

初始的版本库还是和上回一样, 在 `master` 和 `dev` 分支中都有自己的独立修改.

在 `master`创建一个文件后，产生分支，在 `master`中继续创建第二个文件，然后在dev分支中分两次在文件一中进行修改。
```shell 
# 这是 master 的 log
* bf75fad (HEAD -> master) create 2  
* f1e708f create 1
-----------------------------
# 这是 dev 的 log
* 103ebbd (HEAD -> dev) add 2 in dev  
* 7de4a5b add 1 in dev  
* f1e708f create 1
```

当我们想要用 rebase 合并 master 到 dev的时候:
```shell 
$ git branch

# 输出
 *dev
  master
-------------------------
$ git rebase master 

# 输出
First, rewinding head to replay your work on top of it...
Applying: change 3 in dev
Using index info to reconstruct a base tree...
M   1.py
Falling back to patching base and 3-way merge...
Auto-merging 1.py
CONFLICT (content): Merge conflict in 1.py
error: Failed to merge in the changes.
Patch failed at 0001 change 3 in dev
The copy of the patch that failed is found in: .git/rebase-apply/patch

When you have resolved this problem, run "git rebase --continue".
If you prefer to skip this patch, run "git rebase --skip" instead.
To check out the original branch and stop rebasing, run "git rebase --abort".
```

git 发现的我们的 1.py 在 master 和 dev 上的版本是不同的, 所以提示 merge 有冲突. 具体的冲突, git 已经帮我们标记出来, 我们打开 1.py 就能看到:
```shell
a = 1
# I went back to change 1
<<<<<<< f7d2e3a047be4624e83c1265a0946e2e8790f79c
# edited in dev
=======
# edited in master
>>>>>>> change 4 in master
```

这时 HEAD 并没有指向 master 或者 dev, 而是停在了 rebase 模式上:
```shell
$ git branch
* (no branch, rebasing master) # HEAD 在这
  dev
  master
```
所以我们打开 1.py, 手动合并一下两者的不同.
```
a = 1
# I went back to change 1
​
# edited in master and dev
```

然后执行 git add 和 git rebase --continue 就完成了 rebase 的操作了.
```shell
$ git add 1.py
$ git rebase --continue
```
此时来看看dev的log
```shell
* 7f28382 (HEAD -> dev) add 2 in dev  
* 7f26325 add 1 in dev  # 基于现在最新的bf75fad进行修改
* bf75fad (master) create 2  
* f1e708f create 1
```
!! 注意 !! 这个例子也说明了使用 rebase 要万分小心, 千万不要在共享的 branch 中 rebase, 不然就像上面那样, 现在 dev 的历史已经被 rebase 改变了. dev 当中别人提交的 change 就被你无情地修改掉了, 所以千万不要在共享分支中使用 rebase.但你可以选择在rebase后merge到master中
```shell
$ git checkout master
切换到分支 'master'
$ git merge dev
更新 bf75fad..7f28382  
Fast-forward  
1.py | 3 +++  
1 file changed, 3 insertions(+)
```

再来看看 master 的 log:
```shell
$ git log --oneline --graph

# 输出
7f28382 (HEAD -> master, dev) add 2 in dev # dev中的修改被合并到master中，且没有产生分支
7f26325 add 1 in dev  
bf75fad create 2  
f1e708f create 1

```

### (stash）临时修改
假如我们正在进行任务A，但是突然有一个紧急bug修改任务B，但是我并不想把我现在的未完成任务A一起提交或者丢弃，此时我们就可以使用`stash`

```shell
$ git status -s
# 输出
 M 1.py
------------------ 
$ git stash
# 输出
Saved working directory and index state WIP on dev: f7d2e3a change 3 in dev
HEAD is now at f7d2e3a change 3 in dev
-------------------
$ git status
# 输出
On branch dev
nothing to commit, working directory clean  # 干净得很
```
随后我们完成任务B
完成了, 现在可以继续开心的在 `dev` 上刷代码了.

```shell
$ git checkout dev
$ git stash list    # 查看在 stash 中的缓存

# 输出
stash@{0}: WIP on dev: f7d2e3a change 3 in dev
```

上面说明在 `dev` 中, 我们的确有 `stash` 的工作. 现在可以通过 `pop` 来提取这个并继续工作了.

```shell
$ git stash pop

# 输出
On branch dev
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

    modified:   1.py

no changes added to commit (use "git add" and/or "git commit -a")
Dropped refs/stash@{0} (23332b7edc105a579b09b127336240a45756a91c)
----------------------
$ git status -s
# 输出
 M 1.py     # 和最开始一样了
```

## merge和rebase的区别
参考[git rebase的一点理解](https://www.jianshu.com/p/39c45f990c99)
### merge
merge是我们常用的合并分支的命令：
假如开发中：分叉到两个不同的分支，右各自有新的提交：

![image](Pasted%20image%2020210901183914.png "原分支")

当我们使用merge命令合并时，它会把两个分支的最新提交历史（`C3` 和 `C4`）和这个两个分支的最近的祖先（`C2`）进行三方合并，合并的结果就是生成一个新的提交历史。
举例子来说
假如C2共ABC三个文件
甲在master的基础上修改bug，在A中删除了代码，在C中修改了代码
乙创建新分支来增加功能，在B中新增了代码，在C中修改了代码
而后进行merge，基于C2来进行三方合并，于是在A中删除部分代码，在B中新增代码，然后讨论解决一下C中的冲突，创建了C5版本，完成合并

![image](Pasted%20image%2020210901183921.png "基于共同历史C2，进行三方合并")

通过合并操作来整合分叉了的历史。

在将三方合并的时候，总是需要以一个提交历史作为依据的，在这个提交历史的基础上增加其他两个的修改，merge上使用的就是这个两个分支的最近的祖先（`C2`）作为依据。

### rebase
首先我们要理解git的版本管理方式，基于上一个历史版本，存储现在的更改，而后现在的版本又作为下一个版本的历史版本。所以，回溯版本相当于把每一个历史版本的更改依次进行还原，跳转之后的版本相当于把每一次更改再重新做一遍。

rebase这个命令在官方的翻译中意思是：变基。

额，怎么说都有点怪是不是，最后查了几个词典，我觉得把rebase翻译为：重定基底

重定基底有两词语组成：

-   重定：动词，重新确定的意思
-   基底：名词，就是依据，把某种事物作为依托或根据，在git中，这个依据的事物就是**提交历史**

合起来就是：重新确定所依据的提交历史。

rebase同样是通过合并来整合分叉的历史，唯一的不同就是，**合并时所依据的提交历史不同**（基），它是直接拿两个分支的最新提交历史（`C3` 和 `C4`）中的一个作为依据（即基），比如以`C3`为基础，提取在 `C4` 中引入的补丁和修改，然后在 `C3` 的基础上应用一次。

这个过程就相当于改变`C4`的基底为`C3`，并将`C4`上的修改依序应用于`C3` 上，生成新的`C4'`, 这个过程就改变了`C4`的基底，也就是所谓的**变基**。

![image](Pasted%20image%2020210901184802.png "改变C4的基底为C3，并将C4上的修改依序应用于C3 上，生成新的C4'")

将 `C4` 中的修改变基到 `C3` 上。

`git rebase [basebranch][topicbranch]` ， 以basebranch为基，将topicbranch的修改应用于basebranch上。

```shell
$ git checkout experiment
$ git rebase master
First, rewinding head to replay your work on top of it...
Applying: added staged command
```

这时experiment分支的提交历史就已经改变了，master分支在experiment分支之后。

现在回到 `master` 分支，进行一次快进合并。

```shell
$ git checkout master
$ git merge experiment
```

![image](Pasted%20image%2020210901184906.png "变基合并可以让最后只剩下一条主线分支")

此时，C4' 指向的快照就和上面使用 merge 命令的例子中 C5 指向的快照一模一样了。

这两种整合方法的最终结果没有任何区别，但是变基使得提交历史更加整洁。如果开发中使用rebase，可以使得最终的开发版本历史只有一条清晰的主分支，在分支上进行的修改也呈现线性记录。

### 区别
无论是通过变基，还是通过三方合并，最后所生成的结果是一样的，只是他们所生成体提交历史不同。

变基：将一个分支的一系列的提交按顺序应用到另一分支上，前者的所有历史更改被合并为一个大的历史更改保存在历史中。

三方合并：把两方的最后提交合并在一起，因为他们分别的最后提交的版本是基于他们的共同祖先依次迭代更改生成的，所以合并后，每一个分支的所有历史都会被保留。

变基操作的实际是：丢弃一个分支上现有的提交，在另一个分支上新建这些内容但实际上不同的提交。

## 补充
当你进行了修改，但是没有add和commit时，此时切换到其他分支，如果当前的修改会被覆盖，git会进行警告。
