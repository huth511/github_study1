[toc]

---

> Git是版本管理工具的一种，是分布式的控制系统。之前用过SVN，它是中心版本控制系统，与Git有很大的不同，当今主流的版本控制都是用的Git，所以希望借此课程的机会，了解一下Git的使用。

## 一、Git的基础

### 1、Git的基本运作流程

![Git运作流程图]( https://mmbiz.qpic.cn/mmbiz_png/iaf4356mqk5pOvZAOkj35GbXmDOayM0Rwp3mpeLmnE3ruFibU6EWh37zHJbNImu0FMhurgfRDq48ichmdRBCiacjaw/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1 )

#### (1) workspace->index->Repository

​		在本地写的代码都在workspace中，通过add指令暂存到index中，然后通过commit提交到本地仓库Repository中。如果有多位项目成员，则每个成员都对应一套本地仓库管理系统，各自写的代码互不干扰。这也就是分布式的体现，成员之间并行进行，互不干扰。

#### (2) checkout

​		可以切换Repository中的某个分支。这是版本控制的重要功能，在不同分支上工作。

#### (3) pull, push, fetch/clone

​		这是远端Remote与本地之间的数据同步操作。

### 2、Git与SVN的不同

<img src="https://upload-images.jianshu.io/upload_images/1244131-2b4fd4e0dc40d1bb.png" alt="SVN工作图" style="zoom:67%;" />

​		可见SVN并没有本地的仓库，只有一个集中的服务器，所有同步操作直接与服务器进行，这意味着必须要联网才能查看历史版本信息，进行版本控制，而Git拥有本地仓库，本地即有全部的版本历史信息，如果没有网络，只需提交到本地仓库，之后再与Remote同步即可。

​		svn这种集中式十分依赖于中心服务器，缺点不言而喻。Git分布式有去中心化的特点，每个使用者都是平等的，每人都有一套完整的版本库，并且每个人的又有各自修改后写入的新代码。使用者之间可以比较交换，同步。SVN和Git的关系类似于C/S和P2P。

## 二、Git的操作与使用

### 1、Git的基本配置

> Github, Gitee等云平台都是基于Git的，它担任一个托管代码的服务器的角色，但它与SVN中的服务器还是不一样，因为它们与各个主机之间的关系是平等的。

​		**无论是使用Github还是Gitee都需要本地有个Git工具，当与云端服务器同步时，都需要Git与它们通信。**

#### (1) 安装Git
* 先下载安装Git: [https://git-scm.com/download](https://git-scm.com/download);

* 配置用户名邮箱：

  `git config --global user.name "your_name"`

  `git config --global user.email "your_email"`

* 生成SSH Key：

  `ssh-keygen -t rsa -C your_email`

* 查看Key：

  `open ~/.ssh`

  将查到的Key复制下来，这就是公钥，之后会用来配置GitHub/Gitee

#### (2) 配置GitHub

![配置界面](https://upload-images.jianshu.io/upload_images/1244131-af5c10181b9e208e.png)

在GitHub->settings->SSH keys中，如图，粘贴进之前查看到的Key即可。此时Git便可以与Github通信，每次同步Github时不需要再登陆。		

### 2、Git的基本操作

1. git init - - 初始化代码仓库

2. git clone - - 克隆远程仓库
   PS:如果希望在克隆的时候，自己定义要新建的项目目录名称，可以在上面的命令末尾指定新的名字：

   `$ git clone git://github.com/schacon/grit.git mygrit`

3. git add - - 把需要提交的所有修改放到暂存区（Stage）

   - git add file – 提交指定文件
   - git add . || git add -A – 提交所有文件
   - git add *.js – 提交所有.js格式文件
   - git add -f file – 强制添加

4. git diff - - 查看当前目录的所有修改(#当暂存区中没有文件时，git diff比较的是，工作区中的文件与上次提交到版本库中的文件。
   \#当暂存区中有文件时，git diff则比较的是，当前工作区中的文件与暂存区中的文)

   - git diff HEAD - - file – 比较工作区中的文件与版本库中文件的差异。HEAD指向的是版本库中的当前版本，而file指的是当前工作区中的文件。

5. git commit -m “message” - - 提交代码

6. git rm - - 会把文件从当前目录删除（不会保存删除的文件）。如果需要从Git仓库中删除，但保留在当前工作目录中，亦即从跟踪清单中删除，可以使用git rm -r --cached readme.md
   PS:如果一个文件已经被提交到版本库，那么你永远不用担心误删，但是要小心，你只能恢复文件到最新版本，你会丢失最近一次提交后你修改的内容。

7. git log - - 查看历史记录，git log命令显示从最近到最远的提交日志

   - git log --graph – 查看分支合并图

8. git reflog - - 用来记录你的每一次命令

9. git remote - - 查看当前的远程库

10. git remote -v - - 可以显示对应的克隆地址（对于多个远程仓库很有用）

11. git remote add [short_name] - - 可以添加新的远程仓库

12. git remote add origin < address > - - 关联一个远程库

13. git fetch [remote-name] - - 可以从远程仓库抓取数据到本地。

14. git pull - - 更新数据

15. git push [remote_name] [branch_name] - - 推送数据到远程仓库 默认使用origin和master

16. git push -u origin master [-f] - - 第一次将本地库的所有内容推送到远程库上

17. git remote show origin - - 查看远程仓库信息

18. git remote rename [old_name] - - 远程仓库重命名

19. git remote rm [remote_name] - - 删除远程仓库

20. git branch -d < name > - - 删除本地分支

21. git tag - - 显示当前库中的标签

22. git branch - - 可显示当前所有分支。可以使用–merged和–no-merged查看已经合并、未合并的分支。

23. git branch <branch_name> - - 创建新分支

24. git branch -r - - 查看远程仓库分支

25. git checkout <branch_name> - - 切换到指定的分支

26. git checkout -b <branch_name> - - 创建新分支并切换到该分支

27. git merge 合并分支
    举例：
    将hotfix分支合并到master上需要：
    git checkout master
    git merge hotfix
    合并之后可以使用git branch -d hotfix删除分支。
    如果合并时存在冲突，需要手工修改
    合并分支时，加上—no-ff参数就可以用普通模式合并，合并后的历史有分支，能看出来曾经做过合并，而fast forward合并就看不出来曾经做过合并。

28. git checkout . --恢复上次提交状态

    - git checkout --file - - 文件在工作区的修改全部撤销
    - 一种是file修改后还没有被放到暂存区，现在，撤销修改就回到和版本库一模一样的状态；
    - 一种是file已经添加到暂存区后，又作了修改，现在，撤销修改就回到添加到暂存区后的状态。

29. git status – 用于显示工作目录和暂存区的状态。使用此命令能看到那些修改被暂存到了, 哪些没有, 哪些文件没有被Git tracked到。git status不显示已经commit到项目历史中去的信息。

30. git reset --hard HEAD^ - - #版本回退

    - git reset --hard commitId - - 取消回退，commitId为你想要回到的未来版本号
    - PS:Git必须知道当前版本是哪个版本，在Git中，用HEAD表示当前版本，上一个版本就是HEAD，上上一个版本就是HEAD^，当回退版本较早时可以写成HEAD~100。

31. git stash - - 储藏可以获取你工作目录的中间状态——也就是你修改过的被追踪的文件和暂存的变更——并将它保存到一个未完结变更的堆栈中，随时可以重新应用。
    现在你想切换分支，但是你还不想提交你正在进行中的工作；所以你储藏这些变更。为了往堆栈推送一个新的储藏，只要运行git stash。把所有未提交的修改（包括暂存的和非暂存的）都保存起来，用于后续恢复当前工作目录。
    PS:需要说明一点，stash是本地的，不会通过git push命令上传到git server上。

32. git stash list - - 查看现有的所有储藏，此命令显然暗示了git stash可以多次保存工作进度，并用在恢复时候选择。

33. git stash pop [–index] [ < stash > ] - - 重新应用已经实施的储藏（删除储藏）

    - 如果不使用任何参数，会恢复最新保存的工作进度，并将恢复的工作进度从存储的工作进度列表中清除。
    - 如果提供< stash>参数（来自git stash list显示的列表），则从该< stash>中恢复。恢复完毕也将从进度列表中删除< stash>。
    - 选项–index除了恢复工作区的文件外，还尝试恢复暂存区。

34. git stash drop [< stash >] - - 删除一个存储的进度。（默认删除最新的进度）

35. git stash clear - - 清空当前所有的stash

36. git stash branch < branchname > < stash > - - 基于储藏进度创建分支。

## 三、Git的使用案例与心得

### 1、场景一：在本地创建工程

在工程目录里使用：`git init`，便可初始化一个版本库

* 查看本地版本库的状态：

  `git status`

  ![image-20201005161230169](/Users/huth/Library/Application Support/typora-user-images/image-20201005161230169.png)

  如图，可以看到当前本地版本库与remote的库的同步情况（remote操作后面再讲）。

* 开始在本地添加工程文件：

  `git add HomeWork/Git使用心得体会.md`

  此指令会将文件放到暂存区（Index）中，如下图中的Staged Changes：

  ![image-20201005162023873](/Users/huth/Library/Application Support/typora-user-images/image-20201005162023873.png)

* 再提交到本地版本库（Repository）当中：

  `git commit -m "add HomeWork/Git使用心得体会.md"`





https://blog.csdn.net/weixin_43606158/article/details/90729743