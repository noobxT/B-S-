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
## 版本状态和更改历史查询
现在，你已经学会了修改文件，然后把修改提交到Git版本库，现在，再练习一次，修改readme.txt文件如下：
~~~
Git is a distributed version control system.
Git is free software distributed under the GPL.
~~~
然后提交 
~~~
$ git add readme.txt
$ git commit -m "append GPL"
[master 1094adb] append GPL
 1 file changed, 1 insertion(+), 1 deletion(-)
~~~
像这样，你不断对文件进行修改，然后不断提交修改到版本库里，这就好像玩游戏存档，没过关就可以读档重新来过。git也一样，每次修改，git都会提交一个节点（还原点）到版本库，一旦误操作就可以从以前的节点进行恢复。  
现在，我们回顾一下`readme.txt`文件一共有多少个版本提交到了git仓库：  
版本1：wrote a readme file  
```
Git is a version control system.
Git is free software.
```
版本2：add distributed  
```
Git is a distributed version control system.
Git is free software.
```
版本3：append GPL  
```
Git is a distributed version control system.
Git is free software distributed under the GPL.
```
当然git也可以记录历史记录，我们以前做了什么操作，什么时间做的操作都有记录。在git中，我们用`git log`命令查看： 
~~~
$ git log
commit 1094adb7b9b3807259d8cb349e7df1d4d6477073 (HEAD -> master)
Author: Michael Liao <askxuefeng@gmail.com>
Date:   Fri May 18 21:06:15 2018 +0800

    append GPL

commit e475afc93c209a690c39c13a46716e8fa000c366
Author: Michael Liao <askxuefeng@gmail.com>
Date:   Fri May 18 21:03:36 2018 +0800

    add distributed

commit eaadf4e385e865d25c48e7ca9c8395c3f7dfaef0
Author: Michael Liao <askxuefeng@gmail.com>
Date:   Fri May 18 20:59:18 2018 +0800

    wrote a readme file
~~~
我们可以看到我们进行过3次提交修改，最近的一次是`append GPL`,上一次是`add distributed`，最早一次是`wrote a readme file`。  
我们可以在后面加上`--pretty=oneline`来单行显示，看起来更清晰。效果:  
~~~
$ git log --pretty=oneline
1094adb7b9b3807259d8cb349e7df1d4d6477073 (HEAD -> master) append GPL
e475afc93c209a690c39c13a46716e8fa000c366 add distributed
eaadf4e385e865d25c48e7ca9c8395c3f7dfaef0 wrote a readme file
~~~
上面这一大串字母和数字的组合是`commit id`（版本号），可以理解为就是身份证号。git的`commit id`不是递增的数字，而是一个SHA1（一个安全哈希算法）计算
出来的一串数字，用十六进制表示，且所有人的`commit id`都不同。为什么不用单独递增的数字来作为`commit id`？那会造成冲突，如果和其他人在一个组内工作，就会造成ID冲突，那会是个大麻烦！  
## 版本回退
了解了这么多，该进入核心内容了，我们将`readme.txt`回退到上一个版本，也就是`add distributed`那个版本。  
首先，我们看到head指针指到的是`append GPL`版本，也就是ID为`1094ad...`的版本上一个版本就是`HEAD^`，上上一个版本就是`HEAD^^`，当然往上100个版本写100个`^`比较容易数不过来，所以写成`HEAD~100`。  
现在，我们要把当前版本`append GPL`回退到上一个版本`add distributed`,可以使用`git reset`命令：  
~~~
$ git reset --hard HEAD^
HEAD is now at e475afc add distributed
~~~
我们查看一下`readme.txt`内容： 
~~~
$ cat readme.txt
Git is a distributed version control system.
Git is free software distributed under the GPL.
~~~
已经恢复到了`append GPL`的版本,版本回退的时候，仅仅就是讲head指针指向了之前的`append GPL`版本，然后再将工作区的文件更新。  
现在，我又想恢复到新版本怎么办，我们只要知道新版本的`commit id`然后继续沿用上述的命令，就可以回到新版本了。但是我不记得`commit id`了怎么办？  
git提供了一个命令`git reflog`来记录每一次命令：
~~~
$ git reflog
e475afc HEAD@{1}: reset: moving to HEAD^
1094adb (HEAD -> master) HEAD@{2}: commit: append GPL
e475afc HEAD@{3}: commit: add distributed
eaadf4e HEAD@{4}: commit (initial): wrote a readme file
~~~
我们可以看出现在head指针指向的`append GPL`，我也可以查看到最新版本的`commit id`。
## 对版本库的管理修改 
git比其他版本系统控制软件出色的原因就是，git用于管理修改而不是管理文件。
让我们做个试验，第一步，对readme.txt做一个修改，比如加一行内容：
~~~
$ cat readme.txt
Git is a distributed version control system.
Git is free software distributed under the GPL.
Git has a mutable index called stage.
Git tracks changes.
~~~
然后我们添加到缓存区`git add`，并查看一下节点情况`git status`：
~~~
$ git add readme.txt
$ git status
# On branch master
# Changes to be committed:
#   (use "git reset HEAD <file>..." to unstage)
#
#       modified:   readme.txt
#
~~~
然后，再修改readme.txt，改动如下：  
~~~
Git is a distributed version control system.
Git is free software distributed under the GPL.
Git has a mutable index called stage.
Git tracks changes of files.
~~~
提交到版本库`git commit -m""`：
~~~
$ git commit -m "git tracks changes"
[master 519219b] git tracks changes
 1 file changed, 1 insertion(+)
 ~~~
提交后我们再次查看状态：
~~~
$ git status
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

	modified:   readme.txt

no changes added to commit (use "git add" and/or "git commit -a")
~~~
我们前面说了，git管理的修改。当你用`git add`命令后，在工作区的第一次修改就被放到暂存区（缓存区）了，待提交。而接下来的第二次修改并没有提交到暂存区，所以接下来的提交到版本库只是把第一次存到暂存区的修改存到了版本库，而第二次不会提交。
提交流程图示为：
第一次修改→`git add`→第二次修改→`git commit`  
另外，我们可以使用`git diff HEAD -- readme.txt`命令来查看工作区和版本库里最新版本的区别：
~~~
$ git diff HEAD -- readme.txt 
diff --git a/readme.txt b/readme.txt
index 76d770f..a9c5755 100644
--- a/readme.txt
+++ b/readme.txt
@@ -1,4 +1,4 @@
 Git is a distributed version control system.
 Git is free software distributed under the GPL.
 Git has a mutable index called stage.
-Git tracks changes.
+Git tracks changes of files.
~~~
或者我们可以通过`git log -p`命令详细查看具体修改了什么内容。
## 撤销修改
情节1：凌晨2点，kl兄正在写软件的说明文件。由于比较困，在readme.txt中添加了一行：
~~~
$ cat readme.txt
Git is a distributed version control system.
Git is free software distributed under the GPL.
Git has a mutable index called stage.
Git tracks changes of files.
My stupid boss still prefers SVN.
~~~
在提交到版本库之前，KL兄猛然发现自己的错误。想要把工作区文件恢复到上一个版本状态。我们先用`git status`看一下情况：
~~~
$ git status
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

	modified:   readme.txt

no changes added to commit (use "git add" and/or "git commit -a")
~~~
git告诉我们，我们的说明文件没有上传到版本库中，而是对工作区进行了修改。KL兄长出了一口气，工作保住了。接下来我们就要撤销工作区的修改（且git也告诉我们可以进行什么操作）：
我们使用`git checkout -- file`丢掉工作区的修改：  
```
$ git checkout -- readme.txt
```
情节2：上述相同情况，只不过KL兄已经将修改添加到了暂存区，庆幸的是我们没有commit提交到版本库。又一次保住了自己的工作。  
我们再用`git status`查看一下情况。
~~~
$ git status
On branch master
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

	modified:   readme.txt
~~~
git告诉我们可以用`git reset HEAD <file>`把暂存区的修改撤销掉，重新放回工作区：  
~~~
$ git reset HEAD readme.txt
Unstaged changes after reset:
M	readme.txt
~~~
`git reset`命令既可以回退版本，也可以把暂存区的修改回退到工作区。当我们用`HEAD`时，表示最新的版本。  
接下来我们再用再用`git status`查看一下：
```
$ git status
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

	modified:   readme.txt
```
现在暂存区是干净的，工作区有修改。  
我们再将工作区的修改丢弃：  
~~~
$ git checkout -- readme.txt

$ git status
On branch master
nothing to commit, working tree clean
~~~
终于工作保住了。。。。  
情景三：KL兄实在是困得不行，居然提交到了版本库上。怎么办？可以用之前我们讲过的版本回退退到之前的一个版本。我们不赘述。  
情景四：KL兄直接把本地版本库推送到了远程。。嗯。。。。写辞职报告把。。。。    
## 删除文件 

## 创建标签
就算我们有了`commit ID`，我们查找commit的效率还是很低。因为这么一串十六进制数想要找到，也是很浪费时间。所以创建标签就是方便大家的事情。  
# 远程库
## 绑定远程库
有个叫[github]（https://github.com/)的神奇的网站,作为管理代码的仓库。所以github可以作为git的远程仓库。
第一步：我们先创建git的user name和email（如果已创建过，可以跳过此步）：
设置Git的user name和email：
```
$ git config --global user.name "T"
$ git config --global user.email "13134466287wy@gmail.com"
```
第2步：登陆GitHub，打开“Account settings”，“SSH Keys”页面：  
然后，点“Add SSH Key”，填上任意Title，在Key文本框里粘贴`id_rsa.pub`文件的内容
   
    
    
点“Add Key”，你就应该看到已经添加的Key：   
为什么GitHub需要SSH Key呢？因为GitHub需要识别出你推送的提交确实是你推送的，而不是别人冒充的，而Git支持SSH协议，所以，GitHub只要知道了你的公钥，就可以确认只有你自己才能推送。

当然，GitHub允许你添加多个Key。假定你有若干电脑，你一会儿在公司提交，一会儿在家里提交，只要把每台电脑的Key都添加到GitHub，就可以在每台电脑上往GitHub推送了。

最后友情提示，在GitHub上免费托管的Git仓库，任何人都可以看到喔（但只有你自己才能改）。所以，不要把敏感信息放进去。
## 添加远程库  
在github上创建一个git仓库与本地的git仓库进行连接，这样我们既能将github的仓库作为备份，又可以让其他人也通过这个仓库进行协作。    
首先，登陆GitHub，然后，在右上角找到“Create a new repo”按钮，创建一个新的仓库：  
在Repository name填入`learngit`，其他保持默认设置，点击“Create repository”按钮，就成功地创建了一个新的Git仓库：  
目前，在GitHub上的这个`learngit`仓库还是空的，GitHub告诉我们，可以从这个仓库克隆出新的仓库，也可以把一个已有的本地仓库与之关联，然后，把本地仓库的内容推送到GitHub仓库。  
现在，我们根据GitHub的提示，在本地的`learngit`仓库下运行命令：  
~~~
$ git remote add origin git@KLExTtgithub.com:/learngit.git
~~~
请注意，把上面的`KLExTt`替换成你自己的guthub账户名。添加后，远程库的名字就是`orign`，这是git默认的叫法，你也可以改成别的，但是orign这个名字一看就是远程库。  
下一步，就可以把本地库的所有内容推送到远程库上把本地库的内容推送到远程，用`git push`命令，实际上是把当前分支master推送到远程。
由于远程库是空的，我们第一次推送`master`分支时，加上了`-u`参数，Git不但会把本地的master分支内容推送的远程新的master分支，还会把本地的master分支和远程的master分支关联起来，在以后的推送或者拉取时就可以简化命令。  
```
$ git push -u origin master
Counting objects: 20, done.
Delta compression using up to 4 threads.
Compressing objects: 100% (15/15), done.
Writing objects: 100% (20/20), 1.64 KiB | 560.00 KiB/s, done.
Total 20 (delta 5), reused 0 (delta 0)
remote: Resolving deltas: 100% (5/5), done.
To github.com:michaelliao/learngit.git
 * [new branch]      master -> master
Branch 'master' set up to track remote branch 'master' from 'origin'.
```
github的页面内容和本地库已经一模一样了：  
  
  
  
   
如果想在本地再一次做提交到GitHub，直接使用命令`git push`：
~~~
$ git push origin master
~~~
把本地```master```分支的最新修改推送至GitHub，现在，你就拥有了真正的分布式版本库！   
### SSH警告  
当你第一次使用git的`clone`或者`push`命令链接github时，会得到一个警告：
~~~
The authenticity of host 'github.com (xx.xx.xx.xx)' can't be established.
RSA key fingerprint is xx.xx.xx.xx.xx.
Are you sure you want to continue connecting (yes/no)?
~~~
这是因为git使用SSH链接，而SSH链接在第一次验证GitHub服务器的Key时，需要确认你的Key指纹信息，是否真的来自GitHub的服务器，输入`yes`即可。  
git会输出一个警告，告诉你已经把GitHub的Key添加到本机的一个信任列表里了：   
```Warning: Permanently added 'github.com' (RSA) to the list of known hosts.```  
如果你实在担心有人冒充GitHub服务器，输入yes前可以对照[GitHub的RSA Key的指纹信息](https://help.github.com/en/articles/githubs-ssh-key-fingerprints)是否与SSH连接给出的一致。
## 从远程库克隆
现在，假设我们从零开发，那么最好的方式是先创建远程库，然后，从远程库克隆。
首先，登陆GitHub，创建一个新的仓库，名字叫`gitskills`：  
我们勾选`Initialize this repository with a README`，这样GitHub会自动为我们创建一个`README.md`文件。创建完毕后，可以看到`README.md`文件。  
现在，远程库已经准备好了，下一步是用命令git clone克隆一个本地库：
```
$ git clone git@github.com:KLExTt/gitskills.git
Cloning into 'gitskills'...
remote: Counting objects: 3, done.
remote: Total 3 (delta 0), reused 0 (delta 0), pack-reused 3
Receiving objects: 100% (3/3), done.
```
注意把Git库的地址换成你自己的，然后进入gitskills目录看看，已经有README.md文件了：  
```
$ cd gitskills
$ ls
README.md
```










