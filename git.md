# git学习笔记

## 介绍

**学习笔记　和　小白的解决方案的收集**





[阮一峰　ｇｉｔ](http://www.ruanyifeng.com/blog/2015/12/git-cheat-sheet.html)

### 日常使用

我每天使用 Git ，但是很多命令记不住。

一般来说，日常使用只要记住下图6个命令，就可以了。但是熟练使用，恐怕要记住60～100个命令。

![img](http://www.ruanyifeng.com/blogimg/asset/2015/bg2015120901.png)

下面是我整理的常用 Git 命令清单。几个专用名词的译名如下。

> - Workspace：工作区
> - Index / Stage：暂存区
> - Repository：仓库区（或本地仓库）
> - Remote：远程仓库

##### 一、新建代码库

> ```bash
> # 在当前目录新建一个Git代码库
> $ git init
> 
> # 新建一个目录，将其初始化为Git代码库
> $ git init [project-name]
> 
> # 下载一个项目和它的整个代码历史
> $ git clone [url]
> ```

##### 二、配置

Git的设置文件为`.gitconfig`，它可以在用户主目录下（全局配置），也可以在项目目录下（项目配置）。

> ```bash
> # 显示当前的Git配置
> $ git config --list
> 
> # 编辑Git配置文件
> $ git config -e [--global]
> 
> # 设置提交代码时的用户信息
> $ git config [--global] user.name "[name]"
> $ git config [--global] user.email "[email address]"
> ```

##### 三、增加/删除文件

> ```bash
> # 添加指定文件到暂存区
> $ git add [file1] [file2] ...
> 
> # 添加指定目录到暂存区，包括子目录
> $ git add [dir]
> 
> # 添加当前目录的所有文件到暂存区
> $ git add .
> 
> # 添加每个变化前，都会要求确认
> # 对于同一个文件的多处变化，可以实现分次提交
> $ git add -p
> 
> # 删除工作区文件，并且将这次删除放入暂存区
> $ git rm [file1] [file2] ...
> 
> # 停止追踪指定文件，但该文件会保留在工作区
> $ git rm --cached [file]
> 
> # 改名文件，并且将这个改名放入暂存区
> $ git mv [file-original] [file-renamed]
> ```

##### 四、代码提交

> ```bash
> # 提交暂存区到仓库区
> $ git commit -m [message]
> 
> # 提交暂存区的指定文件到仓库区
> $ git commit [file1] [file2] ... -m [message]
> 
> # 提交工作区自上次commit之后的变化，直接到仓库区
> $ git commit -a
> 
> # 提交时显示所有diff信息
> $ git commit -v
> 
> # 使用一次新的commit，替代上一次提交
> # 如果代码没有任何新变化，则用来改写上一次commit的提交信息
> $ git commit --amend -m [message]
> 
> # 重做上一次commit，并包括指定文件的新变化
> $ git commit --amend [file1] [file2] ...
> ```

##### 五、分支

> ```bash
> # 列出所有本地分支
> $ git branch
> 
> # 列出所有远程分支
> $ git branch -r
> 
> # 列出所有本地分支和远程分支
> $ git branch -a
> 
> # 新建一个分支，但依然停留在当前分支
> $ git branch [branch-name]
> 
> # 新建一个分支，并切换到该分支
> $ git checkout -b [branch]
> 
> # 新建一个分支，指向指定commit
> $ git branch [branch] [commit]
> 
> # 新建一个分支，与指定的远程分支建立追踪关系
> $ git branch --track [branch] [remote-branch]
> 
> # 切换到指定分支，并更新工作区
> $ git checkout [branch-name]
> 
> # 切换到上一个分支
> $ git checkout -
> 
> # 建立追踪关系，在现有分支与指定的远程分支之间
> $ git branch --set-upstream [branch] [remote-branch]
> 
> # 合并指定分支到当前分支
> $ git merge [branch]
> 
> # 选择一个commit，合并进当前分支
> $ git cherry-pick [commit]
> 
> # 删除分支
> $ git branch -d [branch-name]
> 
> # 删除远程分支
> $ git push origin --delete [branch-name]
> $ git branch -dr [remote/branch]
> ```

##### 六、标签

> ```bash
> # 列出所有tag
> $ git tag
> 
> # 新建一个tag在当前commit
> $ git tag [tag]
> 
> # 新建一个tag在指定commit
> $ git tag [tag] [commit]
> 
> # 删除本地tag
> $ git tag -d [tag]
> 
> # 删除远程tag
> $ git push origin :refs/tags/[tagName]
> 
> # 查看tag信息
> $ git show [tag]
> 
> # 提交指定tag
> $ git push [remote] [tag]
> 
> # 提交所有tag
> $ git push [remote] --tags
> 
> # 新建一个分支，指向某个tag
> $ git checkout -b [branch] [tag]
> ```

##### 七、查看信息

> ```bash
> # 显示有变更的文件
> $ git status
> 
> # 显示当前分支的版本历史
> $ git log
> 
> # 显示commit历史，以及每次commit发生变更的文件
> $ git log --stat
> 
> # 搜索提交历史，根据关键词
> $ git log -S [keyword]
> 
> # 显示某个commit之后的所有变动，每个commit占据一行
> $ git log [tag] HEAD --pretty=format:%s
> 
> # 显示某个commit之后的所有变动，其"提交说明"必须符合搜索条件
> $ git log [tag] HEAD --grep feature
> 
> # 显示某个文件的版本历史，包括文件改名
> $ git log --follow [file]
> $ git whatchanged [file]
> 
> # 显示指定文件相关的每一次diff
> $ git log -p [file]
> 
> # 显示过去5次提交
> $ git log -5 --pretty --oneline
> 
> # 显示所有提交过的用户，按提交次数排序
> $ git shortlog -sn
> 
> # 显示指定文件是什么人在什么时间修改过
> $ git blame [file]
> 
> # 显示暂存区和工作区的差异
> $ git diff
> 
> # 显示暂存区和上一个commit的差异
> $ git diff --cached [file]
> 
> # 显示工作区与当前分支最新commit之间的差异
> $ git diff HEAD
> 
> # 显示两次提交之间的差异
> $ git diff [first-branch]...[second-branch]
> 
> # 显示今天你写了多少行代码
> $ git diff --shortstat "@{0 day ago}"
> 
> # 显示某次提交的元数据和内容变化
> $ git show [commit]
> 
> # 显示某次提交发生变化的文件
> $ git show --name-only [commit]
> 
> # 显示某次提交时，某个文件的内容
> $ git show [commit]:[filename]
> 
> # 显示当前分支的最近几次提交
> $ git reflog
> ```

##### 八、远程同步

> ```bash
> # 下载远程仓库的所有变动
> $ git fetch [remote]
> 
> # 显示所有远程仓库
> $ git remote -v
> 
> # 显示某个远程仓库的信息
> $ git remote show [remote]
> 
> # 增加一个新的远程仓库，并命名
> $ git remote add [shortname] [url]
> 
> # 取回远程仓库的变化，并与本地分支合并
> $ git pull [remote] [branch]
> 
> # 上传本地指定分支到远程仓库
> $ git push [remote] [branch]
> 
> # 强行推送当前分支到远程仓库，即使有冲突
> $ git push [remote] --force
> 
> # 推送所有分支到远程仓库
> $ git push [remote] --all
> ```

##### 九、撤销

> ```bash
> # 恢复暂存区的指定文件到工作区
> $ git checkout [file]
> 
> # 恢复某个commit的指定文件到暂存区和工作区
> $ git checkout [commit] [file]
> 
> # 恢复暂存区的所有文件到工作区
> $ git checkout .
> 
> # 重置暂存区的指定文件，与上一次commit保持一致，但工作区不变
> $ git reset [file]
> 
> # 重置暂存区与工作区，与上一次commit保持一致
> $ git reset --hard
> 
> # 重置当前分支的指针为指定commit，同时重置暂存区，但工作区不变
> $ git reset [commit]
> 
> # 重置当前分支的HEAD为指定commit，同时重置暂存区和工作区，与指定commit一致
> $ git reset --hard [commit]
> 
> # 重置当前HEAD为指定commit，但保持暂存区和工作区不变
> $ git reset --keep [commit]
> 
> # 新建一个commit，用来撤销指定commit
> # 后者的所有变化都将被前者抵消，并且应用到当前分支
> $ git revert [commit]
> 
> # 暂时将未提交的变化移除，稍后再移入
> $ git stash
> $ git stash pop
> ```

##### 十、其他

> ```bash
> # 生成一个可供发布的压缩包
> $ git archive
> ```



#### GIT BASH操作

1. git clone  [路径] 拉取线上仓库 
2. cd [仓库名] 进入仓库

- 此时在你的仓库路径上会存在一个蓝色的(master);
- ls -a 查看所有的文件 
  此时会发现一个蓝色的.git 文件夹; => 本地仓库;

3. 因为更改了readme所以我们此时需要重新创建一个版本;

   工作区: 你看得见摸得着可以随意操作的代码;
   暂存区: 电话本,知道要把谁放入仓库，同时在暂存区之中会实时对比每次的代码的不同。 

   工作区 => 暂存区 

   git add -A

   指令执行没有任何提示,所以我们需要可视化的查看。

   git status 

   暂存区 => 本地仓库 会创建一个版本,这个版本可以用来回溯;

   git commit -m "注释";

4. 本地版本是本地的!

   如果想要将本地版本推送到线上,这个时候我们需要使用push指令;

   git push -u origin master 

   git 指令起始符 
       push 推送到线上仓库
            -u 全部推送 
               origin 表示一个仓库名称
                     masert  表示主分支

   把主分支全部推送到线上仓库;

5. 如果本地操作不是最新的,我们要git pull 拉取线上仓库代码合并不同的内容然后重新创建版本然后提交。

6. 如果错误删除或者更新代码不要慌使用版本回溯功能帮你忙;

   git reflog => 显示所有的版本

   挑一个你想要回溯的版本;

   回溯之后更新并重新提交到本地仓库;

 ７.　　命令 创建新的分支git branch branchname  不输入分支名字   git branch 是查看当前的分支 命令 git checkout branchname (分支名字)  是切换分支名字

[廖雪疯的教程](https://www.liaoxuefeng.com/wiki/896043488029600)

##　我们要知道的

直接输入`git commit`的时候，或者`git rebase -i`来压缩的时候，都会进入git默认的文本编辑器，根本不会用，然后只能被迫关闭。后得知可以更改文本编辑器，配置如下：

```
git config --global core.editor "\"D:\应用程序\Sublime Text3\sublime_text.exe\""
```

更改后，当git要进入文本编辑器的时候，就会直接打开路径下的sublime text了。

配制后的`C:\Users\admin\.gitconfig`如下:

```
//...略
[core]
    editor = \"D:\\应用程序\\Sublime Text3\\sublime_text.exe\"
```



#### [操作文件及文件夹命令](https://www.cnblogs.com/kongxiaoshuang/p/7088906.html)

\1. cd : 切换到哪个目录下， 如 cd d:\fff  切换 D 盘下面的fff 目录。

　　当我们用cd 进入文件夹时,我们可以使用 通配符*, cd f*,  如果E盘下只有一个f开头的文件夹,它就会进入到这个文件夹.

\2. cd .. 回退到上一个目录， 注意，cd 和两个点点..之间有一个空格。

\3. pwd : 显示当前目录路径。

\4. ls(ll): 都是列出当前目录中的所有文件，只不过ll(两个ll)列出的内容更为详细。

\5. touch : 新建一个文件 如 touch index.js 就会在当前目录下新建一个index.js文件。

\6. rm:  删除一个文件, rm index.js 就会把index.js文件删除.

\7. mkdir: 新建一个目录,就是新建一个文件夹. 如mkdir src 新建src 文件夹.

\8. rm -r : 删除一个文件夹,  rm -r src 删除src目录， 好像不能用通配符。

\9. mv 移动文件, mv index.html src   index.html 是我们要移动的文件, src 是目标文件夹,当然, 这样写,必须保证文件和目标文件夹在同一目录下.

\10. reset 清屏，把git bash命令窗口中的所有内容清空。







#### [在git bush中如何退出vim编辑器](https://www.cnblogs.com/macliu/p/6062917.html)https://i.cnblogs.com/EditPosts.aspx?postid=6062917)

写npm的pakege.json文件的files配置时，如果有不想包含的文件，那就要创建.npmignore文件排除，但windows系统又不允许创建以点开头命名的文件，咋办？

这时候就要用到linux命令行工具创建如git bash。

git bash创建文件和文件夹的命令如下：

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

```
#创建文件
vi

#创建文件    
touch

#拷贝文件
cp

#移动文件
mv

#创建文件夹
mkdir

#另外还有好多命令能够创建文件，之要该命令能够重定向输出到一个不存在的#文件，就会创建文件。例如
tail -f -n 200 /usr/local/tomcat/logs/catalina.out > /tmp/tomcatlog.log 
```

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

 

但是git bush使用vi命令创建文件时进入到vim编辑器后，我不知道怎么退出，查了下发现一个方法：

 

方法：一直按住esc ，再连续按大写的z两次就退出来了。

但实际上，我发现，只要你按住shift键盘，下面的这些命令都可以用：

```
`如果你想编辑某个文档 可以直接编辑的如你有文档AA 可以用``vi` `AA 【注意：必须在AA所在的目录下】``如果没有文档而且你又想编辑就可以直接编辑``vi` `aa【名字你可以随便命名】``也可以先建立一个文档``touch` `aa 然后再编辑``vi` `aa``编辑器有三种模式 1 命令行模式 2 末行模式 3 输入模式``按Esc 就可以进入命令行模式也是系统默认模式``输入模式可以按 o i a 都可以进入 退出可以进入末行和命令行模式``末行模式可以按ctrl+；它的主要功能是退出编辑器 也可以保存退出文档``q! 【强制退出不保存】 q【退出不保存】 wq【退出并保存后面也可以加个！】``在输入模式和命令行模式命令很多 如果你想具体知道哪些你可以在和我说``如复制（yy）粘贴（p) 删除（d）等等`
```

只是，用wq的时候，要先esc，然后按住shift键，出现下面这个界面时才可以输入命令：

![img](https://images2015.cnblogs.com/blog/558786/201611/558786-20161114183645951-572377656.png)





#### 因为中英文互换导致双引号不一致，出现unexpected EOF while looking for matching ""　命令行退不出

bash:syntax error:unexpected end of file

![img](https://img-blog.csdn.net/20180718191406751?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0NpY2kzMDUxMzM2OTky/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)

```
解决方法：ctrl+d


```

















#### git看这篇文章就够了　智哥

   git是一个分布式版本管理工具，和SVN不同的是git把更多的内容放在了**本地仓库**，让本地仓库有了更多的权限，从而不占用网络资源快速地在本地创建各种版本信息，在最终确定版本之后进行统一地推送，**提高了版本管理效率，减轻了网络资源负担**。如下图 : 每个计算机都拥有一个独立的版本库，通过 pull 和 push 等操作对线上进行保存。





​    



![img](https:////upload-images.jianshu.io/upload_images/16960494-ecaa9d5ae6bc8a72.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/534/format/webp)

image

   同时git的线上仓库（或者叫开源社区）也日渐成熟，国内有 `gitee` , 国际上有 `github`,都可以免费地对**私人代码**进行远程托管 ，当然因为网络限制所以github速度有些感人，网络条件不好的小伙伴推荐使用gitee。 这些线上的开源社区中也存在大量的代码供我们学习交流使用，我们也可以开源属于我们的代码，进入一个更大的世界。



![img](https:////upload-images.jianshu.io/upload_images/16960494-91c2377e906e6475.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/141/format/webp)

image.png



![img](https:////upload-images.jianshu.io/upload_images/16960494-2478f5b5731afed2.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/63/format/webp)

image.png

概念上的东西大概说到这里，这些倒是很简单的东西，大家看过理解并记忆就好了。



git版本管理工具的完全使用应以一下几部分内容为核心学习目标，渐进式进行学习 :

1. 本地仓库
2. 远程仓库
3. 分支管理
4. 多人协作

##### before :  gitbash 工具初始配置

   这一步操作可以是说是至关重要的，因为我们需要告知gitbash你的基本信息，便于gitbash去进行记录，在必要的时候进行使用，请注意**这项配置是必须的**, 但是初始配置我们只需要**配置一次即可**,配置的目标是**将用户名和用户邮箱放在全局的配置文件之中**。

配置方式:

```
// 配置全局用户名
$ git config --global user.name "HuaiZhi" 
// 配置全局邮箱号
$ git config --global user.email "123456@qq.com"
```

tip : 如果在以后的使用中出现了带有 `place tell me who you are` 这样的报错，那么就是这两个全局内容没有正确配置，请检查单词是否输入错误，并重新按照以上方法进行设置。

##### part1 : 本地仓库

   本小节的学习大体上分成两个部分，第一部分是如何在本地仓库创建，还原版本，第二部分是要查看本地仓库的基本状态，便于分辨需要进行的操作。

   先用一张图来说明本地仓库我们需要了解的概念。 `工作区` 、`暂存区` 还有 `本地仓库`。



![img](https:////upload-images.jianshu.io/upload_images/16960494-530dd7047bc23f09.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/678/format/webp)

git本地仓库.jpg

不要对陌生的名词感觉到恐惧从而敬而远之，因为这些词往往来自于我们最最基础和简单的代码之中，是最常见的事物。首先需要声明的是，这三个东西对于开发人员完全是没有必要查看的，所以我们暂时将其理解为**三个概念性的内容**，虽然他可以在隐藏文件夹之中找到其本身但是这不是本节课讨论的目标，所以暂时不表，你只需要记住这几个内容的作用就可以了。

**工作区 | workspace**

其实工作区说白了就是我们看得见摸得着可以更改的代码， 基于后面版本的概念我们才会独立出这样一个新的名词，所以这个是最容易理解的东西即:**你所能看到，可以更改的代码即为工作区**

**暂存区 | index**

这个地方是用于存储索引的，**用于决定哪些文件需要进行版本管理**，哪些不需要。因为在项目中我们确实不需要把所有内容都放进版本仓库之中，版本仓库应该只存储我们项目中改变的代码，而一些工具类内容则不需要放入其中，因为工具是稳定且不变的。比如 `node_modules`包之中的内容，我们会 用一个 `.gitignore` 配置文件进行忽略。

**本地仓库 | repository**

这个是**储存代码**和**生成版本**的地方，位于本机硬盘。

基本概念结束了，我们来看一下，如何将你的代码保存在本地仓库之中那 ?

**1.首先你需要一个本地仓库**

我们的版本管理系统是以文件夹 (项目）为单位进行版本管理的，所以我们建立的仓库应该在项目的根目录之中 :

---| project

   xxx.html

   xxx.js

   xxx.xx

先使用gitbash命令行进入到对应的 project  文件夹，然后进行初始化仓库的操作。

```
$ git init 
```

这个操作会创建一个隐藏文件夹， 这个隐藏文件夹是本仓库版本管理系统的全部文件，删除之后可以重新建立新的仓库，当然也意味着本机的所有版本信息，暂存信息，全部消失。**不建议在日常操作中删除该文件夹，请在必要时刻执行删除操作**

初始化之后会在你的根目录中生成如下隐藏文件夹

---| project

   xxx.html

   xxx.js

   xxx.xx

---| `.git`

**2.然后选择需要进行版本控制的文件，将这些文件放入暂存区**

指令，将全部文件放入暂存区:

```
$ git add -A
```

当然我们可以通过在项目中创建 `.gitignore` 来规定不需要版本管理的文件夹或者文件，对必要内容进行忽略

---| project

   xxx.html

   xxx.js

   xxx.xx

   `.gitignore`

---| .git

**.gitignore**

```
node_modules/    这种语法可以忽略文该文件夹下所有内容
*.zip           这种语法可以忽略 *.zip 后缀的所有内容
index.html       当然可以直接编写文件全程
```

当然这个配置是根据你个人需求来进行配置的。

tip : 我们选用 git add 指令配合 .gitignore 就是为了节约我们的使用成本，说白了配置一次就可以一劳永逸，这也是目前的主流添加暂存区方式。  当然更多指令可以使用 git add --help 配合文档进行查看。

**3. 版本提交**

已经决定了哪些文件是可以进行版本管理的，那么之后我们便可以对在暂存区中的内容进行提交并生成一个本地仓库之中的版本，注意在此之前我们是**没有在本地仓库产生一个版本的**。

```
git commit -m "提交注释:这个注释为必须 ，在注释中你要写明你做了哪些改动，因为在版本达到一定数量级的时候，你是无法通过版本号分辨版本的，只能通过注释分辨版本"
```

ok ，如果此时提交成功，那么恭喜你，你已经得到了你的第一个版本了。 这个版本的号码由一个哈希值来标明。

**什么是版本**

其实我们把版本理解成**游戏的存档**即可，在打boss之前我们可能有大概率无法通关，但是如果不存档意味着游戏从头再来，这就是传说中的版本，如果你不玩游戏没法快速理解存档的含义的话，这里还有一个更为通俗的解释。



![img](https:////upload-images.jianshu.io/upload_images/16960494-1ceb107569eba85c.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/623/format/webp)

image.png

你有穿越时间的能力, 可以无限的返回某个时间点，对位置进行无限试错，想一想是不是很爽。 比如你兜里揣着两块钱站在彩票店门口，买了彩票发现没有中奖，怎么办，时间倒流回到你进入彩票站的那一刻，然后重新购买彩票。那么我们把可还原的，进入彩票站的那一刻叫做一个时间节点。在开发过程之中对于代码来说，这可能就是一个具体的版本。



![img](https:////upload-images.jianshu.io/upload_images/16960494-25223bd33ef0e375.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/259/format/webp)

image

~~ps: 本来是在搜索关于时间静止的图片，但是搜出来的图片过于** ， 请未成年人不要轻易搜索~~

**4. 信息查看**

```
$ git status
```

这个指令是查看已经加入暂存区中的内容和工作区内容是否存在差异。

```
$ git reflog 
```

这个指令是查看全部已经产生的版本

通过上述指令可以查看当前工作区中三个部分的状态及任务。

小练习:

1. 更改一下工作区任意内容，然后再去输入`git status` 查看输出内容。
2. git add 将所有内容添加进暂存区之后再去 `git status`查看内容。

**5. 版本还原**

版本还原前提是你必须在本地仓库之中拥有这个版本，我见过最神仙的操作就是刚刚建立好git仓库然后直接把全部项目代码删除了，居然还想要还原 。



![img](https:////upload-images.jianshu.io/upload_images/16960494-b44d4937edc5f281.jpeg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1000/format/webp)

image

如此机智 ， 能活这么大不容易啊。

好了我们说下基本的版本还原知识，如果经历了多次版本提交，`git reflog` 大概会产生如下列表:



![img](https:////upload-images.jianshu.io/upload_images/16960494-912c1926e41fdb83.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/976/format/webp)

git版本.jpg

前面那个黄黄的神秘代码是什么那 ？ 没错他就是 **版本号**，这个版本号是唯一的，这里以七位数的哈希值进行显示，如果我们要回到某个版本的话，可以根据这个代码进行版本回退，当然**回退本身也会产生版本哦**

ok，回退的指令是 :

```
$ git reset --hard  版本号
```

或者回退上一个版本 :

```
$ git reset --hard HEAD^ 一个 ^ 符号代表的就是上一个版本两个 ^ 则代表上上个版本以此类推
```

个人不建议使用第二种回退方式，这种回退方式比较不精准在连续操作中因为回退产生的版本会对版本造成影响，所以不建议使用这种回退方法。

用一张图来总结一下本地仓库 :

指令非常简单 : `add` ，`commit` ，`reset` 共三个，如果你了解了全部概念结合下图，很容易可以学会git工具本地的使用了。



![img](https:////upload-images.jianshu.io/upload_images/16960494-5a7699b9efa1a482.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/763/format/webp)

本地仓库总结.jpg

##### part2 ：远程仓库



![img](https:////upload-images.jianshu.io/upload_images/16960494-73c217b5fd2242f0.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1000/format/webp)

远程仓库.jpg

其实远程仓库就是一个远端的云盘， 这个云盘完整的复制了你的git版本仓库，那么远端在哪那？ 本章节分成两个部分。 `推送` 和`拉取`

###### 推送

**1. 创建远程仓库**

在创建远程仓库的时候，有两个选择，`gitee`  or `github`。

如果考虑效率，并且英文不是很好的小伙伴建议使用 `gitee`，因为 `github` 是全中文的。

[gitee注册页](https://links.jianshu.com/go?to=https%3A%2F%2Fgitee.com%2Fsignup)

[github注册页](https://links.jianshu.com/go?to=https%3A%2F%2Fgithub.com%2Fjoin%3Fsource%3Dheader-home)

请点开链接后自行感受一下，然后再决定选择哪一个，注册结束后登陆并来到主页等待创建一个远程仓库。

1. 新建远程仓库



![img](https:////upload-images.jianshu.io/upload_images/16960494-38e8e60ec5c4257e.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1000/format/webp)

建立仓库.png

1. 填写必要信息



![img](https:////upload-images.jianshu.io/upload_images/16960494-c191488e825b53ff.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/720/format/webp)

建立仓库第二步.jpg

到此为止，你已经拥有了一个属于你的远程仓库了。

**2. 提交远程仓库**

1. 按照上一章节学习内容创建你的本地仓库，创建结束之后在此进行远程仓库链接简写。

```
git remote add origin 你的仓库的名字
```

这个表示给远程仓库 命名为 origin 以后提交的时候这个链接也可以直接使用 origin代替。当然除了origin你还可以随意取名，比如说 o , ori , myOrigin .... 发挥你的想象力，这个只是一个变量名而已。

1. 然后你就可以吧本地仓库中的所有版本内容推送到线上了。

```
git push -u origin master
```

在这里 `origin` 是我们在`remote add` 时添加的远程仓库名称，`master`是分支，我们会在后面章节对分支进行讲解。

如果在这里提示输入账号密码，正常输入账号密码即可。

到了这里你可以在线上仓库刷新一下，并看到，你的项目已经提交上去了。

###### 拉取

如果我们更换电脑或则新加入一个别人完成了一部分的项目，这个时候我们要先得到项目远程仓库之中的代码，来进行继续的开发，那么这个时候我们就需要从远程仓库对代码进行拉取，从而得到之前的代码，版本信息和分支，以便于继续进行开发。

拉取分成三种形态即为 `clone` , `pull` , `fork`， 这三种拉取方式在用途方面的区分也比较明确，下面我们来看一下这几个拉取方式的区别。

**1. clone操作 **

我们来看一下clone的示意图 :



![img](https:////upload-images.jianshu.io/upload_images/16960494-9a23b07ed332728c.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1000/format/webp)

clone示意图.jpg

clone 操作会将线上仓库完整拉取到本地，也就是说你会得到一个和线上一模一样的项目，同时clone操作会建立一个项目文件夹对项目进行包裹。

我们建议 : **在创建仓库的初期使用clone操作，拉取完整线上代码便于继续开发**

指令为 :

```
$ git clone 仓库地址
```

**2.pull 拉取操作**



![img](https:////upload-images.jianshu.io/upload_images/16960494-ac8f8702de67249e.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1000/format/webp)

pull示意图.jpg

   pull操作会将远程仓库的最新代码放入工作区，如果有冲突的话会优先 **自动合并(auto merge)**, 如果自动合并失效，需要手动合并，我们可以根据`VSCODE`自带工具进行手动合并。但是请注意，如果pull之后 自动合并成功会产生一个新的版本，但是**手动合并则不会产生新的版本，需要自行提交之后才会产生新的版本**。也就是说，手动合并之后我们需要重复 `add` `commit`操作，确保本地仓库产生版本之后再做后续擦操作。

pull操作我们在开发时通常会在两种情况下执行 :

1. 在新的一天开始时，不知是否有人更新过代码，那么我们在开发之前应该先执行以下 `git pull` 再进行今天的开发。

2. 在工作结束准备提交代码的时候，我们在`push`之前应该也先`pull`拉取最新代码，进行合并之后进行提交。

   对了请各位小伙伴务必注意不要随意使用`push --force` 指令进行强制提交，这样的话会覆盖团队中其他小伙伴的代码哦。**道路千万条，安全第一条，push不规范，亲人两行泪**

tip : 所有的pull操作其实都是建立在**多人协作**开发时我们才会存在线上代码和本地代码不一致的情况，如果你的项目开发人员只有你一个人的话，那么则不用考虑上述两条pull指令。

pull指令 :

```
git pull 仓库地址(可选，默认拉取仓库origin之中的代码)
```

**3.fork操作**

fork操作示意图



![img](https:////upload-images.jianshu.io/upload_images/16960494-914a82fdda832d36.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/876/format/webp)

fork.jpg

总的来说，这是一种，开源项目协作方式，简单来说就是你有个项目想要更多的陌生开发人员来帮忙一起开发，你耕田来我织布，那么这个时候用到fork可能再合适不过了。 或者你看到别人的优秀项目想要保存在自己的仓库之中方便阅读下源码，那么fork也在适合不过你了， 不建议在**工作环境下使用fork，因为其效率较为底下**。但是对于没有操作权限的仓库来说，我们想要进行二次开发，那么fork则作为唯一的方式进行开发。

说白了fork就是 **自己复制了一份别人的代码到自己的仓库里，自己玩**，玩的开心了，帮人家改了bug了那么你需要跟人家沟通，你代码错了，我要提交一个修改bug的方案， 那么这个时候 **在你更改好的仓库之中，远程操作提交一个pull request**，然后由项目的负责人来决定是否将你的代码放入他的开源项目之中，如果放入了，那么你就是贡献者之一了哦。

当然这些操作不涉及命令行，指令还是原来的指令，只不过需要你在远程仓库的界面上点击 fork按钮就可以了。然后在本地 `clone` , 开发 ， `add` , `commit` , `push`, 心情好了提交一个 `pull request`

作者：公羊无衣

链接：https://www.jianshu.com/p/cc90360f74aa

来源：简书

简书著作权归作者所有，任何形式的转载都请联系作者获得授权并注明出处。

## 操作记录

11320@baobaoComputer MINGW64 /f/MyFile/IProject
$ cd giteework

11320@baobaoComputer MINGW64 /f/MyFile/IProject/giteework
$ git clone https://gitee.com/embaobao/testgit.git
Cloning into 'testgit'...
remote: Enumerating objects: 4, done.
remote: Counting objects: 100% (4/4), done.
remote: Compressing objects: 100% (4/4), done.
remote: Total 4 (delta 0), reused 0 (delta 0)
Unpacking objects: 100% (4/4), done.

11320@baobaoComputer MINGW64 /f/MyFile/IProject/giteework
$ la -a
bash: la: command not found

11320@baobaoComputer MINGW64 /f/MyFile/IProject/giteework
$ ls -a
./  ../  testgit/

11320@baobaoComputer MINGW64 /f/MyFile/IProject/giteework
$ ls
testgit/

11320@baobaoComputer MINGW64 /f/MyFile/IProject/giteework
$ cd testgit

11320@baobaoComputer MINGW64 /f/MyFile/IProject/giteework/testg
$ ls -a
./  ../  .git/  README.en.md  README.md

11320@baobaoComputer MINGW64 /f/MyFile/IProject/giteework/testg
$ pwd
/f/MyFile/IProject/giteework/testgit

11320@baobaoComputer MINGW64 /f/MyFile/IProject/giteework/testg
$ ^C

11320@baobaoComputer MINGW64 /f/MyFile/IProject/giteework/testg
$ git add -a
error: unknown switch `a'
usage: git add [<options>] [--] <pathspec>...

    -n, --dry-run         dry run
    -v, --verbose         be verbose
    
    -i, --interactive     interactive picking
    -p, --patch           select hunks interactively
    -e, --edit            edit current diff and apply
    -f, --force           allow adding otherwise ignored files
    -u, --update          update tracked files
    --renormalize         renormalize EOL of tracked files (imp
    -N, --intent-to-add   record only the fact that the path wi
    -A, --all             add changes from all tracked and untr
    --ignore-removal      ignore paths removed in the working t-all)
    --refresh             don't add, only refresh the index
    --ignore-errors       just skip files which cannot be addeds
    --ignore-missing      check if - even missing - files are i
    --chmod <(+/-)x>      override the executable bit of the li


11320@baobaoComputer MINGW64 /f/MyFile/IProject/giteework/testg
$ git add -A

11320@baobaoComputer MINGW64 /f/MyFile/IProject/giteework/testg
$ 没报错误就是对了
bash: 没报错误就是对了: command not found

11320@baobaoComputer MINGW64 /f/MyFile/IProject/giteework/testg
$ git add -A 是添加所有的文件夹的更改
fatal: pathspec '是添加所有的文件夹的更改' did not match any fi

11320@baobaoComputer MINGW64 /f/MyFile/IProject/giteework/testg
$ git status
On branch master
Your branch is up to date with 'origin/master'.

Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

        modified:   README.md


11320@baobaoComputer MINGW64 /f/MyFile/IProject/giteework/testg
$ git status 是查看状态
On branch master
Your branch is up to date with 'origin/master'.

nothing to commit, working tree clean

11320@baobaoComputer MINGW64 /f/MyFile/IProject/giteework/testg
$ add 命令 是添加到暂存区哦，完成存档。生成一个Hash 值
bash: add: command not found

11320@baobaoComputer MINGW64 /f/MyFile/IProject/giteework/testg
$ 暂存区 会创建版本，这个版本可以回溯（过去）
bash: 暂存区: command not found

11320@baobaoComputer MINGW64 /f/MyFile/IProject/giteework/testg
$ git commit -m"给提交 进行注释，以方便以后查看"
[master 575bc25] “m给提交 进行注释，以方便以后查看
 1 file changed, 45 insertions(+), 1 deletion(-)

11320@baobaoComputer MINGW64 /f/MyFile/IProject/giteework/testg
$ ^C

11320@baobaoComputer MINGW64 /f/MyFile/IProject/giteework/testg
$ 命令 git commit -m"注释"  是保存暂存区的版本到本地库
bash: 命令: command not found

11320@baobaoComputer MINGW64 /f/MyFile/IProject/giteework/testg
$ 命令 git push -u origin master  推送到线上仓库 oringin(别名)
bash: syntax error near unexpected token `('

11320@baobaoComputer MINGW64 /f/MyFile/IProject/giteework/testg
$ git status
On branch master
Your branch is ahead of 'origin/master' by 1 commit.
  (use "git push" to publish your local commits)

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in workin

        modified:   README.md

no changes added to commit (use "git add" and/or "git commit -a

11320@baobaoComputer MINGW64 /f/MyFile/IProject/giteework/testg
$ git add -A

11320@baobaoComputer MINGW64 /f/MyFile/IProject/giteework/testg
$ git status
On branch master
Your branch is ahead of 'origin/master' by 1 commit.
  (use "git push" to publish your local commits)

Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

        modified:   README.md


11320@baobaoComputer MINGW64 /f/MyFile/IProject/giteework/testg
$ git commit -m"学习了push"
[master 29df2ac] 学习了push
 1 file changed, 80 insertions(+), 3 deletions(-)

11320@baobaoComputer MINGW64 /f/MyFile/IProject/giteework/testg
$ git reflog
29df2ac (HEAD -> master) HEAD@{0}: commit: 学习了push
575bc25 HEAD@{1}: commit: “m给提交 进行注释，以方便以后查看
9af507b (origin/master, origin/HEAD) HEAD@{2}: clone: from httpaobao/testgit.git

11320@baobaoComputer MINGW64 /f/MyFile/IProject/giteework/testg
$ 命令版本回溯 git reset --hrad  版本号
git: 'r命令版本回溯' is not a git command. See 'git --help'.

11320@baobaoComputer MINGW64 /f/MyFile/IProject/giteework/testg
$ 命令 git reflog 显示所有版本
bash: 命令: command not found

11320@baobaoComputer MINGW64 /f/MyFile/IProject/giteework/testg
$ git push -u origin master
Counting objects: 6, done.
Delta compression using up to 4 threads.
Compressing objects: 100% (6/6), done.
Writing objects: 100% (6/6), 2.45 KiB | 89.00 KiB/s, done.
Total 6 (delta 1), reused 0 (delta 0)
remote: Powered By Gitee.com
To https://gitee.com/embaobao/testgit.git
   9af507b..29df2ac  master -> master
Branch 'master' set up to track remote branch 'master' from 'or

11320@baobaoComputer MINGW64 /f/MyFile/IProject/giteework/testg
$ git pull
Already up to date.

11320@baobaoComputer MINGW64 /f/MyFile/IProject/giteework/testg
$ git status
On branch master
Your branch is up to date with 'origin/master'.

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in workin

        modified:   README.md

no changes added to commit (use "git add" and/or "git commit -a

11320@baobaoComputer MINGW64 /f/MyFile/IProject/giteework/testg
$ git add -A

11320@baobaoComputer MINGW64 /f/MyFile/IProject/giteework/testg
$ git status
On branch master
Your branch is up to date with 'origin/master'.

Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

        modified:   README.md


11320@baobaoComputer MINGW64 /f/MyFile/IProject/giteework/testg
$ git diff HEAD --readme.md
usage: git diff [<options>] [<commit> [<commit>]] [--] [<path>.

11320@baobaoComputer MINGW64 /f/MyFile/IProject/giteework/testg
$ ls
README.en.md  README.md

11320@baobaoComputer MINGW64 /f/MyFile/IProject/giteework/testg
$ git diff HEAD --README.md
usage: git diff [<options>] [<commit> [<commit>]] [--] [<path>.

11320@baobaoComputer MINGW64 /f/MyFile/IProject/giteework/testg
$ fit -diff HEAD --REDEME.md
bash: fit: command not found

11320@baobaoComputer MINGW64 /f/MyFile/IProject/giteework/testg
$ git status
On branch master
Your branch is up to date with 'origin/master'.

Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

        modified:   README.md


11320@baobaoComputer MINGW64 /f/MyFile/IProject/giteework/testg
$ git checkout
M       README.md
Your branch is up to date with 'origin/master'.

11320@baobaoComputer MINGW64 /f/MyFile/IProject/giteework/testgit (master)
$ git status
On branch master
Your branch is up to date with 'origin/master'.

Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

        modified:   README.md


11320@baobaoComputer MINGW64 /f/MyFile/IProject/giteework/testgit (master)
$ git checkout -- REDA^C

11320@baobaoComputer MINGW64 /f/MyFile/IProject/giteework/testgit (master)
$ git checkout -- README.md

11320@baobaoComputer MINGW64 /f/MyFile/IProject/giteework/testgit (master)
$ git status
On branch master
Your branch is up to date with 'origin/master'.

Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

        modified:   README.md


11320@baobaoComputer MINGW64 /f/MyFile/IProject/giteework/testgit (master)
$ 取消修改 git checkout -- file命令
bash: 取消修改: command not found

11320@baobaoComputer MINGW64 /f/MyFile/IProject/giteework/testgit (master)
$ 命令 git reset HEAD <file>可以把暂存区的修改撤销掉（unstage）
bash: file: No such file or directory















9af507b HEAD@{4}: clone: from https://gitee.com/embaobao/testgi  t.git

11320@baobaoComputer MINGW64 /f/MyFile/IProject/giteework/testg  it (master)
$ git push -u origin master
giCounting objects: 3, done.
Delta compression using up to 4 threads.
Compressing objects: 100% (3/3), done.
Writing objects: 100% (3/3), 12.01 KiB | 1.71 MiB/s, done.
Total 3 (delta 0), reused 0 (delta 0)
remote: Powered By Gitee.com
To https://gitee.com/embaobao/testgit.git
   410ebb4..237c1ef  master -> master
Branch 'master' set up to track remote branch 'master' from 'or  igin'.

11320@baobaoComputer MINGW64 /f/MyFile/IProject/giteework/testg  it (master)
$ git status
On branch master
Your branch is up to date with 'origin/master'.

nothing to commit, working tree clean

11320@baobaoComputer MINGW64 /f/MyFile/IProject/giteework/testg  it (master)
$ clear

11320@baobaoComputer MINGW64 /f/MyFile/IProject/giteework/testg  it (master)
$ cd ..

11320@baobaoComputer MINGW64 /f/MyFile/IProject/giteework
$ cd ..

11320@baobaoComputer MINGW64 /f/MyFile/IProject
$ ls
csharp/  giteework/  js/      sql/  VSCODE/
CTEMP/   gitlern/    nodejs/  VS/

11320@baobaoComputer MINGW64 /f/MyFile/IProject
$ cd gitlern

11320@baobaoComputer MINGW64 /f/MyFile/IProject/gitlern
$ git init
Initialized empty Git repository in F:/MyFile/IProject/gitlern/  .git/

11320@baobaoComputer MINGW64 /f/MyFile/IProject/gitlern (master  )
$ cd ..

11320@baobaoComputer MINGW64 /f/MyFile/IProject
$ ls
csharp/  giteework/  js/      sql/  VSCODE/
CTEMP/   gitlern/    nodejs/  VS/

11320@baobaoComputer MINGW64 /f/MyFile/IProject
$ cd giteework

11320@baobaoComputer MINGW64 /f/MyFile/IProject/giteework
$ ls
learninggit/  testgit/

11320@baobaoComputer MINGW64 /f/MyFile/IProject/giteework
$ cd learninggit

11320@baobaoComputer MINGW64 /f/MyFile/IProject/giteework/learninggit
$ git init 命令是初始化一个库
Initialized empty Git repository in F:/MyFile/IProject/giteework/learninggit/命令是初始化一个库/.git/

11320@baobaoComputer MINGW64 /f/MyFile/IProject/giteework/learninggit
$ git init
Initialized empty Git repository in F:/MyFile/IProject/giteework/learninggit/.git/

11320@baobaoComputer MINGW64 /f/MyFile/IProject/giteework/learninggit (master)
$







11320@baobaoComputer MINGW64 /f/MyFile/IProject/gitlern (master  )
$ cd ..

11320@baobaoComputer MINGW64 /f/MyFile/IProject
$ ls
csharp/  giteework/  js/      sql/  VSCODE/
CTEMP/   gitlern/    nodejs/  VS/

11320@baobaoComputer MINGW64 /f/MyFile/IProject
$ cd giteework

11320@baobaoComputer MINGW64 /f/MyFile/IProject/giteework
$ ls
learninggit/  testgit/

11320@baobaoComputer MINGW64 /f/MyFile/IProject/giteework
$ cd learninggit

11320@baobaoComputer MINGW64 /f/MyFile/IProject/giteework/learninggit
$ git init 命令是初始化一个库
Initialized empty Git repository in F:/MyFile/IProject/giteework/learninggit/命令是初始化一个库/.git/

11320@baobaoComputer MINGW64 /f/MyFile/IProject/giteework/learninggit
$ git init
Initialized empty Git repository in F:/MyFile/IProject/giteework/learninggit/.git/

11320@baobaoComputer MINGW64 /f/MyFile/IProject/giteework/learninggit (master)
$ 命令 创建新的分支git branch branchname  不输入分支名字   git branch 是查看当前的分支 命令 git checkout branchname (分支名字)  是切换分支名字
bash: syntax error near unexpected token `('

11320@baobaoComputer MINGW64 /f/MyFile/IProject/giteework/learninggit (master)
$ 命令 git-merge[分支名] 合并分支
bash: 命令: command not found

11320@baobaoComputer MINGW64 /f/MyFile/IProject/giteework/learninggit (master)
$ git branch gitlearn-zm
fatal: Not a valid object name: 'master'.











11320@baobaoComputer MINGW64 ~
$ cd f:/*gitee
bash: cd: f:/*gitee: No such file or directory

11320@baobaoComputer MINGW64 ~
$ cd f:


11320@baobaoComputer MINGW64 /f
$

11320@baobaoComputer MINGW64 /f
$  cd MyFile/

11320@baobaoComputer MINGW64 /f/MyFile
$ ls
 DeskTopExtention/
 fq/
 IProject/
'QF SOURCE'/
 source/
 切尔诺贝利.Chernobyl.S01E01.中英字幕.WEBrip.720P-人人影视.mp4
 切尔诺贝利.Chernobyl.S01E02.中英字幕.WEBrip.720P-人人影视.mp4
 切尔诺贝利.Chernobyl.S01E03.中英字幕.WEBrip.720P-人人影视.mp4

11320@baobaoComputer MINGW64 /f/MyFile
$ CD IProject
bash: CD: command not found

11320@baobaoComputer MINGW64 /f/MyFile
$ cd IProject

11320@baobaoComputer MINGW64 /f/MyFile/IProject
$ ls
csharp/  CTEMP/  giteework/  gitlern/  js/  nodejs/  sql/  VS/  VSCODE/

11320@baobaoComputer MINGW64 /f/MyFile/IProject
$ cd giteework

11320@baobaoComputer MINGW64 /f/MyFile/IProject/giteework
$ git status
fatal: not a git repository (or any of the parent directories): .git

11320@baobaoComputer MINGW64 /f/MyFile/IProject/giteework
$ pwd
/f/MyFile/IProject/giteework

11320@baobaoComputer MINGW64 /f/MyFile/IProject/giteework
$ git branch
]fatal: not a git repository (or any of the parent directories): .git

11320@baobaoComputer MINGW64 /f/MyFile/IProject/giteework
$ git branch srcnote
fatal: not a git repository (or any of the parent directories): .git

11320@baobaoComputer MINGW64 /f/MyFile/IProject/giteework
$ ls
learninggit/  testgit/

11320@baobaoComputer MINGW64 /f/MyFile/IProject/giteework
$ cd testgit

11320@baobaoComputer MINGW64 /f/MyFile/IProject/giteework/testgit (master)
$ git branch srcnote

11320@baobaoComputer MINGW64 /f/MyFile/IProject/giteework/testgit (master)
$ git branch
* master
  srcnote

11320@baobaoComputer MINGW64 /f/MyFile/IProject/giteework/testgit (master)
$ git checkout src note
error: pathspec 'src' did not match any file(s) known to git.
error: pathspec 'note' did not match any file(s) known to git.

11320@baobaoComputer MINGW64 /f/MyFile/IProject/giteework/testgit (master)
$ git checkout srcnote
Switched to branch 'srcnote'
M       README.md

11320@baobaoComputer MINGW64 /f/MyFile/IProject/giteework/testgit (srcnote)
$ ls
README.en.md  README.md

11320@baobaoComputer MINGW64 /f/MyFile/IProject/giteework/testgit (srcnote)
$ git vim
git: 'vim' is not a git command. See 'git --help'.

The most similar command is
        var

11320@baobaoComputer MINGW64 /f/MyFile/IProject/giteework/testgit (srcnote)
$ git branch -d srnote
error: branch 'srnote' not found.

11320@baobaoComputer MINGW64 /f/MyFile/IProject/giteework/testgit (srcnote)
$ git branch -d srcnote
error: Cannot delete branch 'srcnote' checked out at 'F:/MyFile/IProject/giteework/testgit'

11320@baobaoComputer MINGW64 /f/MyFile/IProject/giteework/testgit (srcnote)
$ git checkout master
Switched to branch 'master'
M       README.md
Your branch is up to date with 'origin/master'.

11320@baobaoComputer MINGW64 /f/MyFile/IProject/giteework/testgit (master)
$ git branch -d srcnote
Deleted branch srcnote (was 237c1ef).

11320@baobaoComputer MINGW64 /f/MyFile/IProject/giteework/testgit (master)
$ git branch
* master

11320@baobaoComputer MINGW64 /f/MyFile/IProject/giteework/testgit (master)
