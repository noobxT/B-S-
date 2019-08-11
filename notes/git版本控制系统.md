# Git的诞生
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
# Git简介
Git是什么？
Git是目前世界上最先进的分布式版本控制系统（没有之一）。
Git有什么特点？简单来说就是：高端大气上档次！
> 个人理解：Git就是版本同步软件，对代码的debug以及后续的更新进行记录并保存为节点。这些节点具有恢复性（可按修改时间向前或向后恢复）且记录了节点修改内容，修改人员以及修改时间。
# 安装git
最早Git是在Linux上开发的，很长一段时间内，Git也只能在Linux和Unix系统上跑。不过，慢慢地有人把它移植到了Windows上。现在，Git可以在Linux、Unix、Mac和Windows这几大平台上正常运行了。

要使用Git，第一步当然是安装Git了。根据你当前使用的平台来阅读下面的文字：
## 在Linux上安装Git  
首先，你可以试着输入git，看看系统有没有安装Git：  
~~~
$ git
The program 'git' is currently not installed. You can install it by typing:
sudo apt-get install git
~~~  
像上面的命令，有很多Linux会友好地告诉你Git没有安装，还会告诉你如何安装Git。
如果你碰巧用Debian或Ubuntu Linux，通过一条```sudo apt-get install git```就可以直接完成Git的安装，非常简单。  
老一点的Debian或Ubuntu Linux，要把命令改为```sudo apt-get install git-core```，因为以前有个软件也叫GIT（GNU Interactive Tools），结果Git就只能叫```git-core```了。由于Git名气实在太大，后来就把GNU Interactive Tools改成```gnuit```，```git-core```正式改为```git```。  
如果是其他Linux版本，可以直接通过源码安装。先从Git官网下载源码，然后解压，依次输入：```./config```，```make```，```sudo make install```这几个命令安装就好了。  
## 在Mac OS X上安装Git
如果你正在使用Mac做开发，有两种安装Git的方法。  
一是安装homebrew，然后通过homebrew安装Git，具体方法请参考homebrew的文档：http://brew.sh//  
第二种方法更简单，也是推荐的方法，就是直接从AppStore安装Xcode，Xcode集成了Git，不过默认没有安装，你需要运行Xcode，选择菜单“Xcode”->“Preferences”，在弹出窗口中找到“Downloads”，选择“Command Line Tools”，点“Install”就可以完成安装了。
Xcode是Apple官方IDE，功能非常强大，是开发Mac和iOS App的必选装备，而且是免费的！  
## 在Windows上安装Git
在Windows上使用Git，可以从Git官网直接[下载安装程序](https://git-scm.com/downloads)，然后按默认选项安装即可。  
安装完成后，在开始菜单里找到“Git”->“Git Bash”，蹦出一个类似命令行窗口的东西，就说明Git安装成功！
安装完成后，还需要最后一步设置，在命令行输入：  
```
$ git config --global user.name "Your Name"
$ git config --global user.email "email@example.com"
```  
因为Git是分布式版本控制系统，所以，每个机器都必须自报家门：你的名字和Email地址。你也许会担心，如果有人故意冒充别人怎么办？这个不必担心，首先我们相信大家都是善良无知的群众，其次，真的有冒充的也是有办法可查的。  
 # 版本库  
## 创建版本库
版本库就是存放管理代码的仓库，存放在版本库里的代码都可以被git修改、删除追踪历史节点。  
首先创建一个版本库：  
~~~
$ mkdir learngit
$ cd learngit
$ pwd
/Users/T/learngit
~~~
> mkdir命令为创建一个文件夹，后面接要创建文件夹的名称。（make directory 的缩写）  
> cd命令为进入某个目录，后面接想要进入文件夹的名称。（change directory 的缩写）  
> pwd命令为显示当前所在目录路径。（print working directory的缩写）  
创建好版本库之后，在版本库目录下有个`.git`的隐藏目录（以免你手贱误操作）。这个目录git来存放节点以及配置文件，不能破坏以及私自修改目录里的文件。   
如需查看目录所有文件：Linux：`ls -la` ,Windows: `dir/a`。  
然后将这个目录通过`git init`命令变成git可以管理的仓库：
~~~
$ git init
Initialized empty Git repository in /Users/michael/learngit/.git/
~~~  
**第二种方法：**  
~~~
$ git init learngit
Initialized empty Git repository in /Users/michael/learngit/.git/
~~~
直接创建目录并作为git的版本库。  
**第三种方法：**
通过`git clone`命令从github拷贝代码到本地git版本库。  
~~~
$ git clone https://github.com/KLExTt/B-S-.git
~~~
## 将文件添加进工作区  
所有版本控制系统只能追踪文本文件，程序代码。所以图片以及视频这些文件是无法追踪修改节点的，但是可以通过版本控制系统进行管理（那谁还用，失去了管理的意义）  
word是也是一种例外，git也无法追踪历史修改节点。  
因为文本是有编码的，而视频图片这些文件属于二进制，没有编码。所以git（包括所有的版本控制系统）都无法追踪历史节点。  
**windows另有玄机**  
当你在window下使用自带记事本进行编辑时，想要保存一个以UTF-8编码的文件就会在文件开始的地方插入三个不可见的字符（0xEF 0xBB 0xBF，即BOM）。它是一串隐藏的字符，用于让记事本等编辑器识别这个文件是否以UTF-8编码。这种做法就是方便了windows自带的记事本软件，给其他语言带来巨大的麻烦。（比如说PHP）  
推荐使用[notepad++](http://notepad-plus-plus.org)或者[editplus](https://www.editplus.com) 来代替记事本。。  
既然知道了，能管理什么和不能管理什么，我们继续。。  
首先随便编写一个txt文件：  
~~~
git is a version control system.
git is a free software.
~~~
然后放到我们刚才创建的工作区`learngit`文件夹里。因为这是git工作区，不放在工作区里，git是无法操作这个文件的。    
接下来通过命令来操作git，添加进仓库：（上述一步只是添加进版本库，git想要追踪这个文件就必须通过命令添加进git）  
~~~
$ git add readme.txt
~~~
再然后，用命令`git commit`将文件提交到仓库：
~~~
$ git commit -m "wrote a readme file"
[master (root-commit) eaadf4e] wrote a readme file
 1 file changed, 2 insertions(+)
 create mode 100644 readme.txt
~~~
这样就完成了。`git commit`可以理解为提交一个节点，或者可以说是一个还原点。`-m`后面双引号中的内容为改动记录。最好详细填写修改原因，这样方便你或者其他人查看你修改了什么内容或者增加了什么东西。  
不想`-m`添加内容也可以`--allow-empty-message`什么都不添加。不推荐这么做。  
git commit命令执行成功后会告诉你，~1 file changed~：1个文件被改动（我们新添加的readme.txt文件）；~2 insertions~：插入了两行内容（readme.txt有两行内容）。   
# 基本操作
## 查询状态
现在我们已经提交了文件到工作区中，接下来我们进入readme.txt修改一下，改为如下内容：  
~~~
Git is a distributed version control system.
Git is free software.
~~~
现在，我们回到git，输入`git status`命令，结果为：
~~~
$ git status
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

	modified:   readme.txt

no changes added to commit (use "git add" and/or "git commit -a")
~~~
`git status`命令可以让我们时刻掌握仓库当前的状态，上面的命令输出告诉我们，`readme.txt`被修改过了，但还没有准备提交的修改。
## 查询修改内容
虽然git告诉我们问文件已经修改过，但是我们不知道修改了什么地方。所以用`git diff`来查看修改内容：  
~~~
$ git diff readme.txt 
diff --git a/readme.txt b/readme.txt
index 46d49bf..9247db6 100644
--- a/readme.txt
+++ b/readme.txt
@@ -1,2 +1,2 @@
-Git is a version control system.
+Git is a distributed version control system.
 Git is free software.
~~~
上面的命令可以看出`-`后面为修改前的内容，`+`为修改后的内容。既然知道了有修改内容，但是需要进行提交并创建节点。  
## 保存修改并创建节点  
在通过上述命令之后，我们已经知道了文件进行了什么修改，所以我们要进行提交到git仓库并创建节点。  
首先，`git add`命令到暂存区（个人理解为缓存）：  
~~~
$ git add readme.txt
~~~
不会有任何输出，在第二步之前，我们先`git status`查看一下仓库状态：
~~~
$ git status
On branch master
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

	modified:   readme.txt
~~~  
`git status`告诉我们，将要被提交的修改包括readme.txt，接下来我们`git commit -m`提交到git，生成一个节点：  
~~~
$ git commit -m "add distributed"
[master e475afc] add distributed
 1 file changed, 1 insertion(+), 1 deletion(-)
 ~~~
接下来我们再用`git status`查看一下仓库状态：
~~~
$ git status
On branch master
nothing to commit, working tree clean
~~~
命令行告诉我们，没用东西需要提交，且暂存区（缓存区）是空的。   
在介绍第二种方法之前我们先来解释一下上文提到的暂存区（缓存区）、版本库和工作区分别指的是什么： 
## 工作区与版本库以及操作流程
**工作区**就是指在电脑里创建的目录，存放等待git操作的文件或者是修改完成的文件。上文创建的`learngit`文件夹就是一个工作区。
**版本库**：暂存区(stage)就属于版本库之中，以及后文将提到的分支和指针`head`。我们上面做的一些添加到版本库的操作就是向master分支去添加。你问我master是啥？master就是个名字，意思是主分支的意思。就像大树有树干和枝杈，master就可以理解为主干。上文描述`.git`的也属于git的版本库之中。 
前面讲了我们把文件往Git版本库里添加的时候，是分两步执行的：  
第一步是用`git add`把文件添加进去，实际上就是把文件修改添加到暂存区；  
第二步是用`git commit`提交更改，实际上就是把暂存区的所有内容提交到当前分支。  
因为我们创建Git版本库时，Git自动为我们创建了唯一一个master分支，所以，现在，`git commit`就是往master分支上提交更改。  
你可以简单理解为，需要提交的文件修改通通放到暂存区，然后，一次性提交暂存区的所有修改。  
俗话说，实践出真知。现在，我们再练习一遍，先对`readme.txt`做个修改，比如加上一行内容：  
~~~
Git is a distributed version control system.
Git is free software.
Git has a mutable index called stage.
~~~
然后，在工作区新增一个`LICENSE`文本文件（内容随便写）。   
先用```git status```查看一下状态：
```
$ git status
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

	modified:   readme.txt

Untracked files:
  (use "git add <file>..." to include in what will be committed)

	LICENSE

no changes added to commit (use "git add" and/or "git commit -a")
```
git告诉我们，`readme.txt`被修改了，而`LICENSE`文件未被添加到版本库保存节点，所以状态是`untracked`。  
现在，使用`git add`，把两个都添加到版本库后，再用`git status`查看一下：  
```
$ git status
On branch master
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

	new file:   LICENSE
	modified:   readme.txt
```
我们可以看出`git add`命令实际上就是把提交的内容放到暂存区（缓存区），然后，执行`git commit`才能提交修改到版本库的分支。  
在我们提交之后，再使用`git status`查看一下状态:  
```
$ git status
On branch master
nothing to commit, working tree clean
```
git告诉我们，没有什么需要提交的，缓存区是空的。    
接着上文说，添加到管理区的**第二种方法**：   
使用`git add .`命令，添加所有已修改的文件到缓存区，然后使用`git commit -m`提交缓存区的所有内容到版本库。
~~~
$ git status
On branch master
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

	new file:   LICENSE
	modified:   readme.txt
~~~


















