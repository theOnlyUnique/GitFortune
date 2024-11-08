# Git 使用教程

# 一、说明

## 1.1 为什么将 Git 作为首位教程

Git 是一款分布式的、可供多人开发的版本控制软件，在多人项目开发当中用于控制项目版本，方便执行该场景下的提交、合并、回退等操作。如果你不会使用 Git，那么你的成员将无法合并你的工作，这对于团队来说是灾难性的。所以新手入门，不管前后端，都应该从 Git 开始了解如何使用 Git！

## 1.2 如何学习本教程及文档中心其他教程

文档中心存在的初衷就是为了后来的学弟学妹可以快速掌握一些基础的知识而搭建的，你们可以在连接好项目组宽带，或者 WIFI 来访问[603 文档中心]()，从这里面访问其它文档资源。

找到文档后可以根据文档指示搭建好对应环境，复制里面的代码或指令自己动手实践，对工具的原理有一定了解并且熟悉常用指令之后就可以熟练运用该工具。所以你们了解工具文档介绍的原理和基础指令即可进入开发。

## 1.3 学习与实践 Git 的方式

在项目中主流的使用 Git 的方式有两种：使用 IDE 的可视化提交按钮和终端指令执行。个人建议是使用终端指令执行 git 操作，这样你可以让自己对 git 的理解更加深刻

# 二、git 运作原理

## 2.1 原理图示与运行流程

![](http://www.ruanyifeng.com/blogimg/asset/2015/bg2015120901.png)

## 2.2 概念补充

-  Workspace：工作区，就是你写代码的 IDE 所看见的区域
-  Index / Stage：暂存区，执行 add 和 stash 之后，你的代码将会被放入该区域，不过 add 会对其进行追踪
-  Repository：本地仓库，执行 commit 之后将记录保存到本地
-  Remote：远程仓库，执行 push 之后将本地的记录与远程对比再合并

## 2.3 文件的状态

-  Git 概念当中的文件状态

![CSDN文章](https://i-blog.csdnimg.cn/blog_migrate/f12a0a47fc6fa0adb800e7a250813c93.png)

**Untracked**: 未跟踪, 此文件在文件夹中, 但并没有加入到 git 库, 不参与版本控制. 通过 git add 状态变为 Staged.

**Unmodify**: 文件已经入库, 未修改, 即版本库中的文件[快照](https://so.csdn.net/so/search?q=快照&spm=1001.2101.3001.7020)内容与文件夹中完全一致. 这种类型的文件有两种去处, 如果它被修改, 而变为 Modified. 如果使用 git rm 移出版本库, 则成为 Untracked 文件

**Modified**: 文件已修改, 仅仅是修改, 并没有进行其他的操作. 这个文件也有两个去处, 通过 git add 可进入暂存 staged 状态, 使用 git checkout 则丢弃修改过, 返回到 unmodify 状态, 这个 git checkout 即从库中取出文件, 覆盖当前修改

**Staged**: 暂存状态. 执行 git commit 则将修改同步到库中, 这时库中的文件和本地文件又变为一致, 文件为 Unmodify 状态. 执行 git reset HEAD filename 取消暂存, 文件状态为 Modified

-  VSCode 当中文件的状态

**U**：Untracked，未追踪，一般是新增文件时出现

**M**：Modified，文件已追踪已修改，但是未进入暂存

**A**：Added,文件已加入暂存区

# 三、项目 Git 常用指令

掌握这部分可以解决项目开发下 90%的场景遇到的问题

# 四、场景举例

## 4.1A

AAAA

## 4.2B

AAAA

## 4.3C

AAAA

# 五、Git 指令大全

## 5.1 项目初始化

-  git init

当你想将自己开发的项目结合上 git 进行版本控制时，可以使用该指令在当前目录创建一个本地仓库以进行版本控制。

此外，可以随便跟一个 name，代表在当前目录创建一个 name 文件夹，再执行`git init`

-  git clone \<url\>

当你想获取别人的代码到本地时，可以使用此指令

## 5.2Git 配置

-  git config --global user.name <"你的昵称，用于显示提交信息">

必填项，配置你的个人信息，不必要实名，显示你的昵称信息，用于提交到远程仓库

-  git config --global user.email <"你的邮箱">

必填项，配置你的邮箱，方便他人联系你

-  git config --list

查看当前 git 的配置

-  git config -e

弹出 git 的配置文件的 txt 文件，供你可视化修改

-  git config --global http.proxy \<127.0.0.1:PORT\>

设置 git 的 http 代理，解决 clone 在 Github 上的项目拉取不下来的问题

-  git config --global https.proxy \<127.0.0.1:PORT\>

设置 git 的 https 代理

-  git config --global --get http.proxy

查看 git 的 http 代理

-  git config --global --get https.proxy

查看 git 的 https 代理

-  git config --global --unset http.proxy

卸载 git 的 http 代理，用于切回国内网络的情况

-  git config --global --unset https.proxy

卸载 git 的 https 代理，用于切回国内网络的情况

## 5.3 项目拉取与推送

-  git fetch origin \<branchName\>

将远程仓库的项目，拉取到本地远程跟踪分支上，该远程跟踪分支表现为`origin/branchName`，相当于一个只读的本地分支。

我们切换到某个分支后，执行`git merge origin/branchName`,即可完成合并。

总的来说，`git fetch`只会将远程分支拉取下来，不会进行合并

-  git pull origin \<remoteBranch\>:\<localBranch\>

相当于执行了`git pull `外加`git merge`,当远程和本地同名时，可以缩写为`git pull origin remoteBranch`

-  git push -u origin \<branchName\>

将本地的 branchName 分支设置为`origin/branchName`分支的上游

-  git push

假如当前分支名为 a，当 a 分支创建了上游，那么在 a 分支执行该命令，会自动将 a 分支推送到远程仓库的上游分支，否则其会提示还未创建上游分支

## 5.4 文件增添与撤销

-  git add \<fileName\>

将某个文件加入暂存区，需要全部加入，可使用`git add .`

-  git checkout \<branchName\>

将当前分支切换到 `branchName`,可以使用`-b`参数应对该分支不存在的情况，以此新建一个分支

-  git checkout [-- \<fileName\>]

将该文件的工作区内容使用缓存区中的内容进行替换，即丢弃当前文件更改

在不和分支名冲突的情况下，`--`可以省略。

使用`git checkout`可以全部撤销

-  git reset

将文件都撤回到上次 commit 时的状态

-  git reset --hard \<hashValue\>

将文件都撤回到上次 commit 时哈希值为 hashValue 时的状态

-  git revert \<hashValue\>

将项目以增量追加的形式恢复到 hashValue 时的状态，commit 会增长

-  git stash

将所有未 commit 的内容加入暂存区，独立放在一起

-  git stash pop

将所有缓存以合并的形式恢复到工作区，有冲突时需要手动解决

## 5.5 分支操作

该部分请查看`文件增添与撤销`,补充一些特殊的指令

-  git branch -a

查看本地所有的分支详情

-  git branch \<branch-name\>

创建一个本地分支，但是不切换

-  git branch -d \<branchName\>

删除一个本地分支

-  git checkout -

返回上一个分支

-  git merge \<branchName\>

将 branchName 合并到当前所在分支

-  git push origin --delete \<branch-name\>

删除远程跟踪分支，另一种写法是`git branch -dr <origin/branch>`

-  git cherry-pick \<hashValue\>

## 5.6 远程仓库指令

-  git remote -v

查看本地的主机配置信息，一般一个主机名会有一对`fetch`和`push`地址

-  git remote add \<host\> \<url\>

对该项目的 host 绑定一个远程仓库地址，如果该主机已经绑定，则会失败。

注意，一个项目可以绑定多个 host，即可以映射多个仓库

-  git remote set-url \<host\> \<newUrl\>

将 host 对应的远程仓库地址进行修改

## 5.7 标签操作

AAAA

# 六、参考链接

1.[图解 Git | 菜鸟教程 (runoob.com)](https://www.runoob.com/w3cnote/git-graphical.html)

2.[gitReference/gitCommands.txt at master · GriefSeed/gitReference](https://github.com/GriefSeed/gitReference/blob/master/gitCommands.txt)

3.[Git_List/README.md at master · ZJF-Coder/Git_List](https://github.com/ZJF-Coder/Git_List/blob/master/README.md)

4.[Git 中文件的 4 种状态\_git 中文件状态-CSDN 博客](https://blog.csdn.net/alan418/article/details/106629307)

5.[Git 分支和文件名重名的时候如何切换分支\_git 新旧版本文件名重复-CSDN 博客](https://blog.csdn.net/weixin_43889618/article/details/119916947)
