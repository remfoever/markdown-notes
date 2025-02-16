# 代码管理工具Git

## git 简介

TortosiseSVN集中式控制系统

Git分布式

## Git的安装和配置

```c
$ git config --global user.email 2579475474@qq.com
$ git config --global user.name "jingtao.cui"   
```

Git可以通过不同的参数，灵活设置这些配置的作用范围。 

● --global：配置～/.gitconfig文件，对当前用户下的所有仓  库有效。

● --system：配置/etc/gitconfig文件，对当前系统下的所有用  户有效。 

● 无参数：配置.git/config文件，只对当前仓库有效。

学习Git，首先要明白几个重要的基本概念：工作区（Working  Directory）、暂存区（Staging Area）和版本库（Repository）。版  本库里保存的是我们提交的多个版本的代码快照，如果你想查看某个  版本的代码，可以通过git checkout命令将版本库里这个版本的代码  拉取出来，释放到工作区。在工作区，你可以浏览某一个版本的代  码、修改代码。如果你想把你的修改保存到版本库中，可以先将你的  修改保存到暂存区，接着修改，再保存到暂存区，直到真正完成修改，再统一将暂存区里所有的修改提交到版本库中，如图所示。

![image-20250216203131293](https://raw.githubusercontent.com/remfoever/md_image_repo/main/image-20250216203131293.png)

为什么还需要一个暂存区呢？将工作区的修改直接提交（Commit），保存到版本库中岂不是更方便？个人理解是：对于一个版本库来说，  你的任何一个提交，包括修改、添加文件、删除文件等操作都会有一个记录，而在实际工作中，对于一个工程师来说，在开发一个功能时，可能会分成很多步，如果每一小步都去提交一次，意义不是很大，而且不是一个完整的功能，别人可能就搞不懂你的提交到底实现了什么功能。如有一个提交：将大象放到冰箱里，别人一看可能就知  道是怎么回事。但在实际的开发过程中，我们可能分步开发。

● 打开冰箱门。  

● 把大象放到冰箱里。  

● 关上冰箱门。  

如果将每次很小的修改都做一次提交，就不是很合适，从原则上讲，我们的每一次提交，都是一个里程碑：要么新增了一个功能，要  么修改了一个Bug，要么优化了一个功能。在实际开发中的每一小步，  都可以先保存到暂存区，等整体功能完成后，再统一提交比较合理。  讲了这么多，为了更快地上手Git，还是给大家演示一遍。  

首先我们新建一个目录tmp，在tmp目录下新建一个C源文件main.c。

```c
$ mkdir ~/tmp
$ cd ~/tmp
$ touch main.c
```

然后在tmp目录下新建一个Git仓库，并将main.c提交到仓库中。

```c
$ git init				创建一个仓库
$ git status			查看工作区状态
$ git add mian.c		将工作区的修改main.c添加到暂存区
$ git status			查看工作区状态
$ git commit -m "init repo ad add mian.c"	将工作区的修改提交到仓库
```

我们可以使用git log来查看提交信息，包括提交的ID、提交作者、提交时间、提交信息说明等。

```c
$ git log
```

如果提交后又修改了main.c文件，想把这个修改再次提交到仓库，可以使用下面的命令。

```c
$ git add mian.c
$ git commit -m "modify mian.c again: add add function"    
```

通过上面的命令，我们可以将main.c的第二次修改提交到本地仓库，然后使用git log或者git show命令来查看我们新的提交信息和修  改变化。其中git show后面的一串数字字符串是每一次提交的commit  ID。

## 创建分支

如果你想让你的提交不影响整个项目，不影响其他人使用，则可以创建一个自己的分支my_branch，切换到my_brancn分支上，然后在这个分支上修改代码就可以了。提交时再将你的修改用上面的方法提交到my_branch分支上。通过这种操作，你的所有修改都提交到你自己创建的分支my_branch上，而不会影响master主分支上的代码，不会影响其他人

```c
$ git branch my_branch							//创建一个新分支 my_brach
$ git checkout my_branch						//切换到新分支 my_branch
$ git commit -m "on my_brach:modify main.c"		//将修改提交到 my_brach    
$ git checkout master							//切换到master分支，在该分支上看不到新的提交信息   
$ git merge my_branch							//将my_branch 分支上的修改合并到master分支       
```

掌握上面的常用命令，我们就可以使用Git进行代码的修改、提交了。除了上面的常用命令，Git还有很多其他更好用的命令，如分支管理、分支的合并和衍合、标签管理等，实际使用场景也远比上面的复杂，如远程仓库的代码拉取和提交、合并提交时的代码冲突等。可以观看《Linux三剑客》视频教程或者参考相关文档自行学习。

















































































































