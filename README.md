# 作业提交流程

我们的《硅谷 live - 智能合约》 课程使用 github 提交和管理作业，因此有必要梳理一下提交作业的流程，官方视频教程《【必看】Github 使用教程》讲述的不够细致和准确，导致很多同学提交作业这最后一步遇到了阻碍。

## 第一步，fork
注册 github 之类的事情就略过了。
打开 https://github.com/linjie-1/guigulive-operation （每期课程可能都不一样，这里是第二期的地址），下图右侧点击 fork，将工程 fork 到自己命名空间下一份。注意主库里除了 master 以外，按照每个同学的学号已经新建了分支，我们提交作业最终要 pr 到自己学号的分支上，**而不是 master 分支上**。
![图1fork](https://github.com/laberat/course/blob/master/img/%E6%99%BA%E8%83%BD%E5%90%88%E7%BA%A6001.png)

fork 成功之后就会进入到自己命名空间下的库地址，此时仍旧可以看到我们将所有主库附带的分支也 fork 了一份。但我们自己只需要使用我们自己学号的分支即可。如下图。
![图2fork成功](https://github.com/laberat/course/blob/master/img/%E6%99%BA%E8%83%BD%E5%90%88%E7%BA%A6002.png)

## 第二步，听课，找到作业要求，完成作业
听课当然主要是看视频。但为了看到作业要求，我们需要每次都把主库的新增内容拉到我们自己的库中。这个操作称之为**更新**。
在第一步 fork 成功后，我们需要把 github 上的内容下载到本地进行处理（假设你起名叫 smartcontract 文件夹），这个操作成为 clone，具体可以自行搜索clone 操作。总之这时候的状态就是同样的一份文件，存在于三个地方，（1）老董的 github，我们称为主库（2）你自己的 github，我们称为从库（3）你电脑上的smartcontract文件夹下的这个文件。

> 我们提交作业，就是先把修改了的或者新增的作业文件从本地提交到从库，在从从库 pr 到主库的自己学号的分支。

继续来说更新，主库产生了修改或者新增之后，我们需要将这份改动同步到从库里，再拉取到本地，这样才能保持三份文件的一致，在此基础上你才能写作业。以下命令用于更新操作，需要在命令行中操作（图形界面版的期待有其他同学能给出一份吧。。。）：

### 2.1 设置远端库的上游

```
➜  guigulive-operation git:(master) gst
On branch master
Your branch is up-to-date with 'origin/master'.
nothing to commit, working tree clean
➜  guigulive-operation git:(master) git remote -v
origin	git@github.com:laberat/guigulive-operation.git (fetch)
origin	git@github.com:laberat/guigulive-operation.git (push)
➜  guigulive-operation git:(master) git remote add upstream git@github.com:linjie-1/guigulive-operation.git
➜  guigulive-operation git:(master) git remote -v
origin	git@github.com:laberat/guigulive-operation.git (fetch)
origin	git@github.com:laberat/guigulive-operation.git (push)
upstream	git@github.com:linjie-1/guigulive-operation.git (fetch)
upstream	git@github.com:linjie-1/guigulive-operation.git (push)
```
1. gst命令是 `git status` 命令的缩写，用于查看当前 git 仓库的状态，我的结果显示我的 git 库本地和远端（即从库）保持一致
2. `git remote -v` 用于检查当前本地 git 库是在追踪远程的什么库，也就是查看远程库的地址
3. `git remote add upstream` git@github.com:linjie-1/guigulive-operation.git 这句话的意思是我将老董的主库地址设置为我当前远程库的上游。上游很显然符合主从这种关系，也就是老董的库先发生了什么改变，然后我去同步这种改变。fork 操作之后都会有上下游的关系，也就是主从库的关系。
4. 再次使用 `git remote -v` 操作能看到我的远端库（从库）地址，及其上游地址（主库地址）

### 2.2 从上游获取最新的更新到本地

```
➜  guigulive-operation git:(master) git fetch upstream
remote: Counting objects: 1368, done.
remote: Compressing objects: 100% (6/6), done.
remote: Total 1368 (delta 25), reused 23 (delta 23), pack-reused 1339
Receiving objects: 100% (1368/1368), 323.75 KiB | 30.00 KiB/s, done.
Resolving deltas: 100% (221/221), completed with 7 local objects.
From github.com:linjie-1/guigulive-operation
 * [new branch]      1-崔津            -> upstream/1-崔津
 * [new branch]      10-周冠群        -> upstream/10-周冠群
 * [new branch]      100-汪博          -> upstream/100-汪博
 * [new branch]      101-韦建          -> upstream/101-韦建
 * [new branch]      102-刘宇          -> upstream/102-刘宇
 * [new branch]      11-张晓雯        -> upstream/11-张晓雯
 * [new branch]      12-高翔           -> upstream/12-高翔
 * [new branch]      13-熊雄           -> upstream/13-熊雄
 * [new branch]      14-jinnyxie         -> upstream/14-jinnyxie
 * [new branch]      15-张烨           -> upstream/15-张烨
 * [new branch]      16-温家宝        -> upstream/16-温家宝
 ...
```
1. `git fetch upstream` 操作是从上面已经设置好的 upstream，也就是上游库（主库）获取到最新的更新并下载到本地。

### 2.3 合并刚才下载的更新

```
➜  guigulive-operation git:(master) git merge upstream/master
Removing 测试
Merge made by the 'recursive' strategy.
 Lesson2/README.md            |  16 +++++++
 Lesson2/assignment/README.md |  10 +++++
 Lesson2/assignment/yours.sol |   1 +
 Lesson2/orgin/README.md      |   3 ++
 Lesson2/orgin/payroll.sol    |  50 +++++++++++++++++++++
 README.md                    | 104 ++++++++++++++++++++++++++++++++++++++++++-
 lesson1/README.md            |   7 ++-
 lesson1/assignment/README.md |   2 +-
 lesson1/orgin/README.md      |   2 +-
 "\346\265\213\350\257\225"   |   1 -
 10 files changed, 190 insertions(+), 6 deletions(-)
 create mode 100644 Lesson2/README.md
 create mode 100644 Lesson2/assignment/README.md
 create mode 100644 Lesson2/assignment/yours.sol
 create mode 100644 Lesson2/orgin/README.md
 create mode 100644 Lesson2/orgin/payroll.sol
 delete mode 100644 "\346\265\213\350\257\225"
```
1. `git merge upstream/master` 会将上游库的 master 分支与我们当前的 master 分支合并，这样我们就能看到老董最新一节课的作业和源代码了。

### 2.4 可选，推送更新到从库中

```
➜  guigulive-operation git:(master) git push origin master
Counting objects: 122, done.
Delta compression using up to 8 threads.
Compressing objects: 100% (100/100), done.
Writing objects: 100% (122/122), 33.26 KiB | 0 bytes/s, done.
Total 122 (delta 15), reused 117 (delta 14)
remote: Resolving deltas: 100% (15/15), done.
To github.com:laberat/guigulive-operation.git
   a4e63c8..549e92b  master -> master
```
我们可以选择将刚才从主库拉取到的更新推送给我们的从库的 master 分支，当然你也可以选择不这么操作。因为我们交作业不打算使用 master 分支。

## 第三步 提交作业到我们从库的学号分支

第二步最后说到，我们不打算使用 master 分支交作业，为什么？
实际上如果你是助教的身份，这个问题就很好回答了。助教是从 pr 中查看我们的作业的。而 pr 的页面会显示三部分内容，分别是pr 本身的描述、pr 对应的 commits 以及 pr 对应的 file changes。通过查看file changes，助教可以非常清楚的看到我们修改了什么内容，从而完成批作业。
但使用 master 进行作业提交，会混入很多老董讲课的讲义以及很多同学的错误提交等等内容，导致 pr 内容混乱不清，修改作业异常麻烦。

那么我们怎么操作呢？
### 3.0 完成作业
首先，根据 master 中的新的课程内容和作业要求，写出一份可以运行在 remix 上的作业，然后再执行后面的任务。

### 3.1 从主库自己学号分支中拉取最新更新

```
➜  guigulive-operation git:(28-衣云驰) git fetch upstream
remote: Counting objects: 40, done.
remote: Compressing objects: 100% (7/7), done.
remote: Total 40 (delta 1), reused 4 (delta 0), pack-reused 33
Unpacking objects: 100% (40/40), done.
From github.com:linjie-1/guigulive-operation
   5b49acc..dcd0d9b  66-屈小波 -> upstream/66-屈小波
➜  guigulive-operation git:(28-衣云驰) git merge upstream/28-衣云驰
Updating 5c804ee..d506ea7
Fast-forward
 README.md                                           |  2 +-
 lesson1/README.md                                   | 11 +++++++++++
pragma solidity ^0.4.0;
 lesson1/assignment/README.md                        |  6 ++++++
 lesson1/assignment/payroll-yyc.sol                  | 48 ++++++++++++++++++++++++++++++++++++++++++++++++
 lesson1/orgin/README.md                             |  3 +++
    // add
 lesson1/orgin/payroll.sol                           | 49 +++++++++++++++++++++++++++++++++++++++++++++++++
 "\346\265\213\350\257\225"                          |  1 +
 "\350\275\257\344\273\266\346\265\213\350\257\2251" |  2 --
 8 files changed, 119 insertions(+), 3 deletions(-)
 create mode 100644 lesson1/README.md
 create mode 100644 lesson1/assignment/README.md
 create mode 100644 lesson1/assignment/payroll-yyc.sol
 create mode 100644 lesson1/orgin/README.md
 create mode 100644 lesson1/orgin/payroll.sol
 create mode 100644 "\346\265\213\350\257\225"
 delete mode 100644 "\350\275\257\344\273\266\346\265\213\350\257\2251"
➜  guigulive-operation git:(28-衣云驰) gst
On branch 28-衣云驰
Your branch is ahead of 'origin/28-衣云驰' by 27 commits.
  (use "git push" to publish your local commits)
```
在本地的自己学号的分支上（本地切换分支请自行搜索，git checkout 分支名）执行：
- git fetch upstream
- git merge upstream/学号分支名

### 3.2 提交作业
