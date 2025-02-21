# Git指令

### 1. **确认当前目录是否是 Git 仓库**

运行以下命令检查当前目录是否是 Git 仓库：

```bash
git status
```

### 2. **初始化一个新的 Git 仓库**

如果当前目录不是 Git 仓库，你可以将其初始化为一个新的 Git 仓库：

```bash
git init
```

这会在当前目录下创建一个 `.git` 文件夹，表示该目录已经是一个 Git 仓库

### 3. **克隆一个现有的 Git 仓库**

如果你是想在一个现有的远程仓库中工作，可以使用 `git clone` 命令将远程仓库克隆到本地：

bash

复制

```
git clone <远程仓库的URL>
```

例如：

```
git clone https://github.com/你的用户名/你的仓库名.git
```

这会将远程仓库的内容下载到当前目录，并自动将其初始化为 Git 仓库。

------

### 4. **检查是否在正确的目录中操作**

如果你已经初始化了 Git 仓库，但仍然遇到这个错误，可能是因为你在错误的目录中运行了 Git 命令。确保你进入了正确的目录：

```
cd /path/to/your/repository
```

然后再次运行 Git 命令。

------

### 5. **检查父目录是否是 Git 仓库**

Git 会从当前目录向上查找 `.git` 文件夹。如果你在一个子目录中操作，但父目录是 Git 仓库，Git 仍然可以正常工作。你可以运行以下命令检查：

```bash
git rev-parse --show-toplevel
```

这会显示当前 Git 仓库的根目录路径。









#### 1. **添加未跟踪的文件到暂存区**

如果你希望将 `PicGo_config/` 文件夹添加到 Git 仓库中，可以运行以下命令：

```
git add PicGo_config/
```

这将把 `PicGo_config/` 文件夹及其内容添加到暂存区。

------

#### 2. **提交更改**

将文件添加到暂存区后，你需要提交这些更改：

```
git commit -m "添加 PicGo_config 文件夹"
```

------

#### 3. **推送到远程仓库**

如果你希望将这些更改推送到远程仓库（例如 GitHub），可以运行：

```
git push origin main
```

------

#### 4. **忽略未跟踪的文件（可选）**

如果你不希望跟踪 `PicGo_config/` 文件夹，可以通过 `.gitignore` 文件将其忽略：

1. 创建或编辑 `.gitignore` 文件：

   ```
   nano .gitignore
   ```

2. 在文件中添加以下内容：

   ```
   PicGo_config/
   ```

3. 保存并退出编辑器。

这样，`PicGo_config/` 文件夹将不会被 Git 跟踪。

------

#### 5. **检查状态**

完成上述操作后，你可以再次运行 `git status` 检查仓库状态：

```
git status
```

如果没有其他未跟踪的文件或未提交的更改，输出应该是：

```
On branch main
Your branch is up to date with 'origin/main'.

nothing to commit, working tree clean
```







要确认你的本地仓库是否是最新状态，以及如何拉取远程仓库的最新更改，可以按照以下步骤操作：

------

### 1. **检查本地仓库状态**

运行以下命令查看当前分支的状态：

```
git status
```

如果输出显示 `Your branch is up to date with 'origin/main'`，说明你的本地分支已经与远程分支同步，是最新状态。

如果显示 `Your branch is behind 'origin/main'`，说明本地分支落后于远程分支，需要拉取最新更改。

------

### 2. **拉取远程仓库的最新更改**

如果本地分支落后于远程分支，可以使用以下命令拉取最新更改：

```
git pull origin main
```

- `git pull` 会自动从远程仓库（`origin`）的 `main` 分支拉取最新更改，并尝试合并到当前分支。
- 如果有冲突，Git 会提示你解决冲突。

------

### 3. **查看远程仓库的更新**

如果你想查看远程仓库是否有更新，而不直接拉取，可以使用：

```
git fetch origin
```

- `git fetch` 会从远程仓库下载最新的提交和分支信息，但不会自动合并到本地分支。

- 运行后，你可以通过以下命令比较本地分支和远程分支的差异：

  ```
  git log main..origin/main --oneline
  ```

  这会显示远程分支有而本地分支没有的提交。

------

### 4. **合并远程更改**

如果你使用了 `git fetch`，可以手动合并远程分支的更改：

```
git merge origin/main
```

这会将 `origin/main` 的更改合并到当前分支。

------

### 5. **解决冲突（如果有）**

如果在拉取或合并过程中出现冲突，Git 会提示你哪些文件有冲突。你需要手动解决冲突：

1. 打开冲突文件，找到冲突标记（`<<<<<<<`、`=======`、`>>>>>>>`）。

2. 修改文件，保留需要的更改，删除冲突标记。

3. 保存文件后，将解决冲突的文件添加到暂存区：

   ```
   git add <冲突文件>
   ```

4. 完成冲突解决后，提交更改：

   ```
   git commit -m "解决合并冲突"
   ```

------

### 6. **总结**

- 使用 `git status` 检查本地分支是否是最新状态。
- 使用 `git pull origin main` 拉取远程仓库的最新更改。
- 使用 `git fetch` 查看远程仓库的更新，然后手动合并。
- 如果有冲突，手动解决冲突并提交。







# 锋哥git使用教程

```bash
git add .
git commit -m "my modify"
    
git pull		//拉取最新分支
git checkout -b personal/zhangfeng/uart

vi wx_main.c

//esc退出编辑，:wq


git status

git add .

//创建两个新文件
vi a.c
vi b.c
//查看修改了哪些文件
git status

git add a.c
git add b.c
//不想修改了，回退本地上一个版本
git restore --staged a.c


//上交本地仓库
git commit -m "i add two file and modify the wx_main.c"

//查找日志
git log

//压缩日志
git rebase -i HEAD-3  (压缩几条命令)

//再次上传
git push

//强推到远端
git push -f 


//切到主线分支
git checkout master
git pull


git merge master
git status


git merge --commit



//rebase方法解决冲突

git checkout master
git pull
git checkout personal/zhangfeng
git rebase master


//删除分支
git branch -D 分支名





```



![image-20250217232855769](Git%E5%91%BD%E4%BB%A4.assets/image-20250217232855769.png)





