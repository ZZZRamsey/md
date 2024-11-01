命令行展示展示 UI ：posh-Git



注意不同操作系统下的换行符区别：
warning: in the working copy of 'file1.txt', LF will be replaced by CRLF the next time Git touches it



暂存区的内容提交后还是可以查看 （git ls-files） 到，要使用 git status 来看哪些没有被提交。



[十分钟学会正确的 github 工作流，和开源作者们使用同一套流程_哔哩哔哩_bilibili](https://www.bilibili.com/video/BV19e4y1q7JJ/?spm_id_from=333.337.search-card.all.click&vd_source=3659941460e6c74679750d458eaa5726)



**.git文件夹保存着git的所有信息，在移动仓库的时候要把.git文件夹一起移动，才可以被git管理**



## 如何把开源项目拉下来，放到自己的仓库中

要把GitHub上的开源项目放到自己的仓库中进行修改和版本管理，你需要经历以下几个步骤：

1. **Fork 项目**：

   - 登录你的GitHub账户。
   - 找到你想要修改的开源项目，点击页面右上角的 "Fork" 按钮。这将会在你的GitHub账户下创建一个该项目的副本。

2. **克隆项目到本地**：

   - 在你的本地机器上打开命令行工具（如Git Bash或者Terminal）。

   - 使用`git clone`命令来克隆你刚刚Fork的项目到本地目录。例如：

     ```sh
     git clone https://github.com/你的用户名/项目名.git
     ```
   
3. **添加上游仓库**：

   - 为了能够获取原项目的更新，你需要添加原项目的URL为远程仓库。可以通过下面的命令来添加：

     ```sh
     cd 项目名
     git remote add upstream https://github.com/原作者用户名/项目名.git
     # 同理也可以设置origin
     ```

4. **拉取最新更改**：

   - 在开始做任何修改之前，最好先从原项目拉取最新的更改，确保你的本地副本是最新的。

     ```sh
     git checkout main  # 或者 master，取决于默认分支是什么
     git pull upstream main  # 或者 master
     ```

5. **进行修改**：

   - 在本地进行你所需的任何修改。可以使用你喜欢的代码编辑器或IDE来编辑文件。

6. **提交更改**：

   - 当你完成修改后，使用`git add`添加更改到暂存区，然后使用`git commit`提交更改。

     ```sh
     git add .
     git commit -m "你的提交信息"
     ```
   
7. **推送更改到你的仓库**：

   - 使用`git push`命令将你的更改推送到你在GitHub上的仓库。

     ```sh
     git push origin main  # 或者 master
     ```

8. **保持同步**：

   - 如果原项目有新的更新，你可以随时通过 `git pull upstream main` 获取这些更新，并解决可能的合并冲突。
   - 然后再 `git push` 把你的更改推送到你的仓库。

以上步骤可以帮助你将GitHub上的开源项目放到自己的仓库中进行修改，并且进行版本管理。记得在进行任何合并操作前，检查是否有未提交的更改，以免丢失工作。



## 克隆或者拉取远程仓库的某一个分支

要克隆GitHub上仓库的特定分支，你可以使用以下命令：

```bash
git clone -b 分支名 仓库的SSH或HTTPS链接
```

例如，如果你想克隆名为`feature/new-feature`的分支，你可以这样做：

```bash
git clone -b feature/new-feature https://github.com/username/repository.git
```

这将创建一个名为`repository`的本地目录，并检出`feature/new-feature`分支。请确保将`username`替换为仓库所有者的用户名，将`repository`替换为仓库的名称。

如果你已经有了仓库的克隆，但想要切换到不同的分支，你可以使用`git checkout`命令：

```bash
git checkout 分支名
```

例如：

```bash
git checkout feature/new-feature
git checkout origin/video
```

这将切换到`feature/new-feature`分支。如果你在克隆时没有指定分支，它将默认克隆仓库的默认分支（通常是`main`或`master`）。



tips：

如果你在克隆仓库时只拉取了默认的`main`分支，而没有拉取其他分支，那么在你的本地仓库中确实只会有`main`分支。如果你想要查看远程仓库中的其他分支，你可以使用`git branch -a`命令，这将列出所有本地和远程的分支。

如果你想要切换到远程仓库中的另一个分支，你可以使用`git checkout`命令，但是首先你需要确保你已经从远程仓库中获取了所有分支的信息。你可以使用`git fetch`命令来获取远程仓库的所有分支信息，然后再使用`git checkout`命令来切换到你想要的分支。

例如，如果你想要切换到名为`feature/new-feature`的分支，你可以这样做：

```bash
git fetch origin
git checkout -b feature/new-feature origin/feature/new-feature
```

这将从远程仓库`origin`中获取所有分支信息，并创建一个名为`feature/new-feature`的本地分支，跟踪远程仓库中的`feature/new-feature`分支。

如果你在执行这些操作时遇到任何问题，请确保你有足够的权限访问远程仓库（可能需要在平台上配置公钥），并且你的网络连接正常（proxy）。







#### Gitee：Github 加速克隆代码

1. 在 [Gitee](https://www.wangdu.site/?golink=aHR0cHM6Ly9naXRlZS5jb20v) 注册账号
2. 在个人首页头像旁点击 **+** 号，选择**从 Github/Gitlab 导入仓库**

![在这里插入图片描述](https://raw.githubusercontent.com/ZZZRamsey/PicGo_save/main/202409171931862.png?token=AVDP3DESOFSFTQ7P63L5MG3G5FUNY)

1. 在地址栏输入 GitHub 上的 clone 地址即可。

![img](https://raw.githubusercontent.com/ZZZRamsey/PicGo_save/main/202409171933904.png?token=AVDP3DCUMRPAUIQBYTOV2VTG5FUTO)

![img](https://raw.githubusercontent.com/ZZZRamsey/PicGo_save/main/202409171932641.png?token=AVDP3DHV4C2TS4CSIAVKMHDG5FURK)



## git lfs

Git LFS（Large File Storage）是一个 Git 扩展，它的主要作用是帮助管理仓库中的大文件，特别是那些不适合直接放在 Git 仓库中的二进制文件，比如图像、视频、音频文件以及其他大型二进制资产。Git LFS 的核心优点在于它允许你在 Git 仓库中存储大文件的同时，保持仓库的轻量级和高效。

#### 主要功能和优势

1. **缩小仓库大小**：Git LFS 通过将大文件替换成一个小型的文本指针文件，而将实际的大文件内容存储在远程服务器上。这减少了本地 Git 仓库的大小，使得克隆仓库更快，也节省了本地存储空间。
2. **高效的网络传输**：由于只传输指针文件，而不是实际的大文件内容，因此在进行推送（push）和拉取（pull）操作时，网络传输效率更高。
3. **版本控制大文件**：虽然 Git 本身非常适合管理文本文件，但对于大文件来说，传统的 Git 可能会变得低效。Git LFS 解决了这个问题，使得版本控制大文件成为可能。
4. **易于集成**：Git LFS 是一个开源项目，支持多种平台，并且很容易集成到现有的 Git 工作流中。
5. **无缝协作**：团队成员可以像平常一样使用 Git，而无需担心大文件带来的问题，因为 <u>Git LFS 自动处理了大文件的存储和恢复。</u>

#### 工作原理

当你在使用 Git LFS 的仓库中添加了一个被标记为使用 LFS 的大文件时，Git LFS 会上传该文件到远程存储库，并在本地仓库中留下一个指向该文件的指针文件。这个指针文件包含了文件的 SHA256 校验和、文件大小和其他元数据。<u>当其他用户克隆或拉取仓库时，他们也会得到这些指针文件，并且 Git LFS 会自动下载对应的大文件。</u>

#### 使用场景

- **多媒体开发**：如果你的项目包含大量的图像、视频或音频文件，Git LFS 可以帮助你更好地管理这些文件。
- **二进制文件管理**：对于包含编译后的二进制文件或其他大型二进制资源的项目，Git LFS 提供了一种有效的解决方案。
- **任何包含大文件的项目**：只要项目中有不适合直接放入 Git 仓库的大文件，Git LFS 都可以作为一个很好的解决方案。





以下两条命令分别用于不同的目的，下面是对它们的具体解释：

#### `git-lfs install`

这条命令用于初始化 Git LFS 的工作环境。它会做以下几件事情：

1. **安装 Git LFS 的钩子（hooks）**：这些钩子是 Git LFS 用来拦截 Git 命令（如 `commit` 和 `clone`）并在适当时候调用 Git LFS 的脚本，以处理大型文件的存储和检索。
2. **配置 Git LFS**：确保 Git LFS 被正确配置以便与你的 Git 客户端一起工作。

执行此命令后，Git LFS 会被设置好，使得在你进行 Git 操作时，Git LFS 可以自动管理那些被标记为使用 LFS 的文件。

#### `git-lfs pull`

这条命令用于从远程仓库中拉取 Git LFS 文件，并将它们恢复成实际的内容文件。具体来说：

1. **拉取 LFS 文件**：从远程仓库获取那些被 Git LFS 替换为小的文本指针文件的实际内容。
2. **替换指针文件**：将存储在远程仓库中的实际文件内容下载并替换掉本地的指针文件。

这条命令确保你的本地副本包含了所有实际的大文件，而不是只有指针文件。

#### 举例说明

假设你在一个使用 Git LFS 的项目中工作：

1. **安装 Git LFS**：

   ```sh
   git lfs install
   ```

   这将确保 Git LFS 的钩子被安装到了你的 Git 环境中。

2. **拉取 LFS 文件**：

   ```sh
   git lfs pull
   ```

   这将下载所有缺失的 LFS 文件到你的本地仓库，使你能够访问这些大文件。

#### 结合使用

通常情况下，如果你在一个新的环境中开始工作，并且知道你要处理的仓库使用了 Git LFS，你可能需要先运行 `git-lfs install` 来准备环境，然后使用 `git-lfs pull` 来确保所有的大文件都被下载到本地。





## 确定一个仓库是否使用了git lfs

要确定一个 Git 仓库是否使用了 Git LFS，你可以通过几个方面来进行检查：

### 1. 检查 `.gitattributes` 文件

Git LFS 通过 `.gitattributes` 文件来指定哪些文件应该使用 LFS 存储。你可以查看仓库根目录下的 `.gitattributes` 文件是否存在以及是否包含了 Git LFS 的配置。

```sh
cat .gitattributes
```

如果文件中有类似这样的行：

```sh
*.bin filter=lfs diff=lfs merge=lfs -text
```

这就意味着扩展名为 `.bin` 的文件被配置为使用 Git LFS。

### 2. 检查 Git 钩子（hooks）

Git LFS 安装时会在仓库的 `.git/hooks` 目录下放置一些钩子脚本。你可以检查这个目录看看是否有 Git LFS 的钩子存在。

```sh
ls .git/hooks
```

如果看到像 `pre-push`、`post-checkout`、`post-merge` 等脚本，并且这些脚本看起来是 Git LFS 提供的，那么这个仓库很可能在使用 Git LFS。

### 3. 检查 Git LFS 日志

你可以使用 Git LFS 的命令来查看 LFS 文件的状态。

```sh
git lfs status
```

这条命令会显示仓库中哪些文件正在被 Git LFS 管理。

### 4. 检查 Git LFS 跟踪的文件

使用 `git lfs track` 命令可以查看 Git LFS 当前正在跟踪的文件模式。

```sh
git lfs track
```

如果命令返回了一些文件模式，那么这些文件类型就是被 Git LFS 管理的。

### 5. 检查仓库历史记录

如果你有仓库的访问权限，可以查看仓库的历史记录，看看是否有使用 Git LFS 的提交记录。

```
git log --follow -- *.bin
```

这里以 `.bin` 文件为例，如果有使用 Git LFS 的历史记录，可能会看到一些关于 LFS 的提交信息。

### 6. 检查远程仓库

如果你可以访问远程仓库，也可以检查远程仓库是否有 `.gitattributes` 文件，或者查看远程仓库的提交历史中是否有 Git LFS 的相关提交。

通过上述方法之一，你可以判断一个仓库是否使用了 Git LFS。如果发现仓库使用了 Git LFS，那么在进行操作时就需要确保 Git LFS 是安装并且配置好的。







## 创建一个新的分支

git 使用哈希值来标识每一个版本。

当你运行 `git checkout -b dev 8908` 这样的命令时，你实际上是在尝试基于特定提交创建一个新的分支。但是，这里的 "8908" 看起来不是一个完整的提交哈希值，通常提交哈希是由一串字母和数字组成的较长字符串。

正确的命令格式应该是这样的：

```sh
git checkout -b <new-branch-name> <commit-hash>
```

这里的 `<commit-hash>` 应该是完整的或至少是足以区分的提交哈希值的一部分。例如：

```sh
git checkout -b dev 8908abc123def4567890abcdef1234567890abcdef
# 或者，如果 "8908abc" 已经足够区分
git checkout -b dev 8908abc
```

这条命令做了两件事：

1. 它创建了一个名为 `dev` 的新分支。
2. 它将新分支的起点设置为指定的提交哈希值对应的提交，这意味着新分支将从此提交开始，而不是从当前分支的最新提交开始。

如果你不确定 "8908" 对应的完整提交哈希值，你可以使用 `git log` 或者 `git reflog` 来查找。一旦找到了正确的提交哈希值，你就可以使用上述命令来基于那个提交创建新分支了。





## git中的submodule

Git submodule是一种机制，它允许在一个Git仓库中嵌入另一个Git仓库作为一个子目录。这使得你可以将一个独立的Git项目作为另一个项目的子目录来跟踪。以下是submodule与普通文件之间的几个关键区别：

#### Git submodule的特点

- **独立版本控制**：每个submodule都是一个独立的Git仓库，有自己的提交历史。这意味着你可以为每个submodule指定特定的版本或提交，而不必更新整个项目。
- **引用远程仓库**：submodule可以引用一个远程Git仓库，这样即使submodule本身没有被克隆，你也可以通过简单的命令来获取它。
- **依赖管理**：submodule非常适合用来管理项目的依赖关系，特别是当这些依赖关系本身也在不断开发和维护时。
- **版本锁定**：你可以锁定submodule到特定的提交，确保项目的依赖关系保持一致。

#### Git submodule与普通文件的关系

- **存储方式**：普通文件直接存储在主仓库中，而submodule则是在本地存储一个指向其版本库的链接（通常是`.git`目录），实际的版本库内容存储在`.git/modules`目录下。
- **版本控制**：普通文件的每次修改都会记录在主仓库的历史中；而submodule的修改只会在主仓库中记录为指向submodule的新提交的引用。
- **操作方式**：对普通文件的操作可以直接通过Git命令完成，而submodule需要使用专门的`git submodule`命令来进行初始化、更新和同步。
- **共享内容**：普通文件直接包含在项目中，而submodule可以用来共享代码片段或库，这些代码片段或库可以在多个项目中重用。

#### 示例

假设你有一个主项目`project-main`，并且它依赖于一个库`lib-a`。你可以将`lib-a`作为一个submodule添加到`project-main`中，这样`lib-a`将作为一个独立的Git仓库存在于`project-main/lib-a`目录下。当你克隆`project-main`时，`lib-a`并不会自动被克隆下来，你需要使用`git submodule update --init`来获取它。

总之，Git submodule提供了一种方法来管理项目之间的依赖关系，尤其是当这些依赖关系本身也是活跃的开发项目时。然而，submodule也有其局限性，比如增加了项目的复杂度和初始化的步骤，因此在某些情况下，人们可能会选择使用其他工具或方法来管理依赖，比如包管理器。





## 文件没有被写到.gitignore中，但却不受git管理

报错1：

git代码提交时，有一个目录下的文件一直识别不出来（add、commit 都是没有clean的），但是在目录下有文件，重新pull代码，目录下是空的，添加代码文件后，再次add、commit还是空的；

报错2：

Git在添加目录时遇到了Fatal: unpopulated submodule的解决办法
今天，在把以前的一个目录整体拷贝到git的目录下时，在add的时候遇到了报错，提示unpopulated submodule的信息，无法添加。后来经过查证，可以采用如下的方法解决.

报错3：

fatal: Pathspec 'au.py' is in submodule 'administer'



`git rm` ： **同时从工作区和索引中删除文件**。即本地的文件也被删除了。

`git rm --cached` ： **从索引中删除文件。但是本地文件还存在**， 只是不希望这个文件被版本控制。

出现报错的原因：一直识别不出来的那个文件夹，之前是一个gitmodule，或者他本身之前没有被git管理，是一个空文件夹。在里面添加东西之后，git并不会识别新添加的东西，而是只根据缓存中的状态，所以先从索引中删除一下对应文件，然后再添加一下就可以了。

针对提示的目录papers

```bash
git rm -rf --cached folder/

git add folder/
```



参考： [【Git】Git出现 fatal: Pathspec ‘xxx‘ is in submodule ‘xxx‘ 异常 解决方案_pathspec is in submodule-CSDN博客](https://blog.csdn.net/zzddada/article/details/121930030) 





## git diff





## git 查看当前已有分支

要查看当前已有的本地分支，你可以使用 `git branch` 命令。这里有几种不同的方式来查看本地分支：

1. **列出所有本地分支**：

   ```bash
   git branch
   ```

   这个命令会列出所有本地分支，并在当前所在的分支前面加上一个星号 (`*`)。

2. **列出所有本地分支（不带星号）**：

   ```bash
   git branch --no-color
   ```

   如果你不希望输出带有颜色标记，可以使用 `--no-color` 选项。

3. **列出所有本地分支和远程分支**：

   ```bash
   git branch -a
   ```

   这个命令会列出所有本地分支以及远程分支。

4. **查看当前分支**：

   ```bash
   git branch --show-current
   ```

   这个命令会显示当前所在的分支名称。

5. **查看当前分支的详细信息**：

   ```bash
   git branch --verbose
   ```

   这个命令会列出所有本地分支，并附带最近一次提交的哈希值和提交信息。

6. **查看当前分支与远程分支的关联情况**：

   ```bash
   git branch -vv
   ```

   这个命令会列出所有本地分支，并显示最近一次提交的哈希值、提交信息以及与远程分支的关联情况。

选择其中一个命令执行即可查看所需的分支列表。



## git 切换分支

[git 学习笔记 —— 保留/丢弃当前分支修改并切换至其他分支 - yhjoker - 博客园 (cnblogs.com)](https://www.cnblogs.com/yhjoker/p/11776240.html)

#### checkout和switch的区别

`git checkout` 和 `git switch` 都是用来切换分支的Git命令，但它们有一些关键的区别：

1. **历史和默认行为**:
   - `git checkout`: 这个命令在Git早期版本中就已经存在，用于切换分支，但它也有其他功能，比如可以用来恢复文件到之前的提交状态，或者从一个分支中检出文件到工作目录。
   - `git switch`: 这个命令是在Git 2.23版本中引入的，目的是为了提供一个更清晰和专门用于切换分支的命令。它避免了`git checkout`的一些混淆行为，如同时用于切换分支和恢复文件。
2. **语义清晰度**:
   - `git checkout` 的多用途可能会导致一些混乱，尤其是对于Git的新用户来说，因为它不仅用于切换分支，还能用于其他操作。
   - `git switch` 的设计更加专注于分支切换，这使得其用途更为明确，减少了误用的可能性。
3. **创建并切换分支**:
   - `git checkout -b <new-branch>`: 这个组合命令可以在创建新分支的同时切换到这个新分支。
   - `git switch -c <new-branch>`: 类似地，`git switch` 也有一个组合命令来创建并立即切换到新分支。
4. **未来方向**:
   - Git社区引入`git switch`和`git restore`命令的意图是逐步淘汰`git checkout`的部分功能，使其功能更加纯粹，只用于文件的检出和恢复，而分支切换则完全交给`git switch`。

总的来说，`git switch`是为了提高命令的专一性和易用性而设计的，而`git checkout`则是一个多功能命令，可能包含了你不需要的额外行为。随着Git的发展，推荐使用`git switch`进行分支切换，以获得更清晰的行为和更好的用户体验。



#### 临时切换到某个提交查看

要在 Git 中临时切换到某个特定的提交记录进行查看，而不改变当前分支的工作状态，你可以使用 `git checkout` 命令结合 `--detach` 选项。下面是一些步骤和命令示例：

1. **首先确认你要查看的提交的哈希值**。可以通过 `git log` 查看提交历史来找到它。

2. **使用以下命令切换到该提交**:

   ```
   git checkout --detach <commit-hash>
   ```

3. **在这个临时状态下，你可以自由地查看文件、运行程序等**。

4. **当你完成查看后，可以使用 `git reflog` 找回最近操作过的分支**：

   ```
   git reflog
   ```

5. **最后，使用 `git checkout` 切换回原来的分支**:

   ```
   git checkout <branch-name>
   ```

这样，你就能够在不干扰当前工作分支的情况下，临时查看任何历史提交的内容了。



## git stash不确定新的修改需不需要，暂存

如果你不希望立即提交修改，但又想保留它们，你可以使用 `git stash save "message"` 命令来存储当前工作目录的状态。<u>执行之后，本地代码会恢复到未修改之前的状态（上一个版本），自动执行了reset</u>

这会将所有未暂存和未提交的修改存放到一个堆栈中，你可以稍后使用 `git stash pop` 或 `git stash apply` 来恢复这些修改。



#### 查看当前暂存的修改（stash）

1. **查看 stash 列表**：使用 `git stash list` 命令查看当前所有的 stash 记录。这会列出所有暂存的更改及其描述。

   ```
   git stash list
   ```

2. **查看特定 stash 的内容**：如果你想查看某个特定 stash 的具体内容，可以使用 `git stash show` 命令加上 stash 的编号。例如：

   ```
   git stash show stash@{0}
   ```

#### 删除暂存的修改（stash）

1. **删除特定的 stash**：如果你想删除某个特定的 stash，可以使用 `git stash drop` 命令加上 stash 的编号。例如，删除最近一次的 stash：

   ```
   git stash drop stash@{0}
   ```

2. **删除所有 stash**：如果你想删除所有 stash，可以使用 `git stash clear` 命令。

   ```
   git stash clear
   ```





## git 将修改的文件添加到暂存区，而不添加未追踪的文件

```sh
git add --update
```

这个命令会将所有已经被跟踪的文件（即已经被加入过版本控制的文件）中那些有修改的部分添加到暂存区，而不会触碰那些未被跟踪的新文件。

如果你想要确认哪些文件被添加到了暂存区，可以运行：

```sh
git status
```

这会显示当前仓库的状态，包括哪些文件已经被添加到暂存区，哪些文件还未被跟踪。





## 将已添加到暂存区的文件移回工作区

要从 Git 的暂存区（staging area）中移除所有文件并将它们移回工作区，你可以使用 `git reset` 命令。以下是具体的步骤：

- 使用`git reset`命令可以将暂存区中的所有文件移回工作目录。

  ```
  git reset .
  ```

这条命令会将暂存区的所有改动移回到工作目录，但不会删除任何文件。这样，所有被暂存的文件都会被取消暂存，并且保留它们在工作区中的状态。

如果需要移除暂存区中的特定文件，可以指定文件路径：

```
git reset <file-path>
```



## 已添加到暂存区的文件，再次发生修改或者删除

当文件已经被添加到暂存区（也称为索引区），如果这些文件之后又被修改或删除，情况会有所不同：

1. **文件被修改**：
   - 如果一个文件已经被添加到暂存区，然后在这个文件上进行了进一步的修改，那么这些额外的修改不会自动反映到暂存区中。
   - 这意味着暂存区中保存的是最后一次添加时的状态。
   - 如果你需要将这些额外的修改加入暂存区，你需要重新执行 `git add` 命令。
2. **文件被删除**：
   - 如果一个文件被添加到了暂存区，然后这个文件被删除，Git 会认为这个文件在暂存区中存在，但在工作目录中不存在。
   - 在这种情况下，如果你执行 `git commit`，该文件会被记录为已删除。

### 处理方法

#### 对于被修改的文件

- 如果你想将修改后的文件重新添加到暂存区，可以使用：

  ```
  git add <file-path>
  ```

- 如果你想取消暂存某个文件，可以使用：

  ```
  git reset <file-path>
  ```

- 如果你想取消暂存所有文件，可以使用：

  ```
  git reset .
  ```

#### 对于被删除的文件

- 如果你想将删除的文件从暂存区中移除，可以使用：

  ```
  git reset <file-path>
  ```

- 如果你想恢复删除的文件，可以使用：

  ```
  git checkout <file-path>
  ```

- 如果你想忽略文件的删除状态并直接提交，可以直接执行 `git commit`。这会将文件记录为已删除。

通过上述命令，你可以根据需要管理已经被添加到暂存区的文件。



## git 推送个人分支到远程仓库（关联远程仓库）

如果你想将本地分支与远程分支建立跟踪关系，可以使用 `--set-upstream` 或者 `-u` 选项。这个选项通常用在 `git push` 命令中，以指定本地分支应该跟踪哪个远程分支。这样做的好处是，以后你可以直接使用 `git push` 或 `git pull` 而不需要每次都指定远程和分支名。

#### 示例

假设你有一个本地分支 `main` 并且想要将其与远程仓库中的 `main` 分支关联起来，你可以执行以下命令：

```
git push -u origin main
```

这里的 `-u` 或 `--set-upstream` 选项会创建一个持久的跟踪关系，使得以后你可以简单地使用：

```
git push
```

或者

```
git pull
```

而不需要每次都指定远程和分支名。

#### 注意事项

- 如果你之前从未推送过这个分支到远程仓库，那么首次使用 `git push -u origin <branch>` 时，它会自动创建一个远程分支。
- 如果远程分支已经存在，那么 `git push -u origin <branch>` 会推送本地分支的更改到远程分支。
- 如果你已经推送过一次，再次使用 `git push -u origin <branch>` 时，它会检查本地分支是否已经跟踪了远程分支，如果没有则会自动设置跟踪关系。



tips：在本地是分叉分支，在远程是单独的分支



```bash
git push origin my_feature 
```

1. **指定远程仓库**:
   - `origin` 是你正在推送更改的远程仓库的名字。通常，`origin` 是指你克隆仓库时指向的原始仓库。
2. **指定本地分支**:
   - `my-feature` 是你本地的分支名称。这是你正在从本地仓库推送到远程仓库的分支。
3. **推送分支到远程仓库**:
   - 这条命令会将 `my-feature` 分支的本地提交历史推送到远程仓库 `origin` 上对应的 `my-feature` 分支。如果远程仓库上不存在这个分支，这条命令会创建一个新的分支。

**注意事项**:

- **权限问题**: 确保你有权限向远程仓库推送更改。对于某些仓库，你可能需要特定的权限才能推送。
- **分支存在性**: 如果远程仓库上还没有 `my-feature` 分支，这条命令会创建它。如果远程仓库上已经有这个分支，这条命令会更新它。
- **冲突**: 如果在你尝试推送期间，远程分支有其他人做了推送，你可能需要先拉取远程的更改 (`git pull origin my-feature`) 并解决任何潜在的合并冲突，然后再重新推送。
- **强制推送**: 如果你想要覆盖远程分支的历史（例如，如果你已经重写了历史），你可以使用 `git push origin my-feature --force` 或 `git push -f origin my-feature`。但是，这通常不推荐，除非你确定这样做不会导致其他人的工作丢失。
- **设置追踪**: 如果这是你第一次推送 `my-feature` 分支到 `origin`，这条命令也会自动设置这个分支的远程追踪信息，使得未来的 `git pull` 和 `git push` 命令能够正确地与远程分支交互。

确保在执行推送操作前，你已经充分测试了你的更改，并且你理解推送的后果。推送操作会将你的更改分享给团队中的其他成员，因此应当谨慎对待。





## 配置远程公钥

在 Linux 系统中，查看 SSH 公钥和私钥的方法非常简单。通常 SSH 密钥对是由 `ssh-keygen` 命令生成的，公钥和私钥默认保存在用户主目录的 `.ssh` 目录下，分别命名为 `id_rsa.pub` 和 `id_rsa`。

#### 查看公钥

1. **打开终端**。

2. **导航到 `.ssh` 目录**（如果不在当前目录下）：

   ```
   cd ~/.ssh
   ```

3. **使用文本编辑器或 `cat` 命令查看公钥**：

   ```
   cat id_rsa.pub
   ```

   或者

   ```
   less id_rsa.pub
   ```

公钥文件的内容通常看起来像这样：

```
ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQC2... [更多密钥内容] user@your-hostname
```

#### 查看私钥

对于私钥，由于它包含敏感信息，通常会被设置为只读，并且可能要求输入密码（passphrase）才能查看。

1. **同样导航到 `.ssh` 目录**：

   ```
   cd ~/.ssh
   ```

2. **使用文本编辑器查看私钥**：

   ```
   cat id_rsa
   ```



## 处理远程仓库的更新（rebase）

### 方法一

```bash
git pull origin master
```

1. **从远程仓库拉取数据**:
   - `origin` 是你指定的远程仓库，通常是你的项目克隆自的那个仓库。
   - `master` 是你希望从远程仓库拉取的分支。在很多项目中，`master` 或 `main` 分支代表项目的主干或稳定版本。
2. **合并远程分支到当前分支**:
   - 这条命令不仅会从远程仓库下载最新的提交，还会将远程 `master` 分支的更改合并到你当前所在的本地分支中。如果你当前也在 `master` 分支上，那么远程的更改将直接合并到你的本地 `master` 分支。

**注意事项**:

- **检查当前状态**: 在执行 `git pull` 命令之前，确保你的工作区没有未提交的更改，或者你已经将这些更改暂存或提交。如果有未提交的更改，`git pull` 可能会导致合并冲突。
- **解决冲突**: 如果远程分支和你的本地分支之间存在冲突，`git pull` 会停止并要求你手动解决这些冲突。解决冲突后，你需要使用 `git add` 和 `git commit` 来完成合并过程。
- **自动设置追踪**: 如果你从未从远程仓库拉取过 `master` 分支，`git pull` 会自动设置本地 `master` 分支追踪远程 `origin/master` 分支。
- **替代命令**: 如果你经常从远程仓库拉取数据，你可能想要使用 `git fetch` 命令来先获取远程更改，再决定是否合并。`git fetch origin master` 会下载远程更改，但不会自动合并。之后，你可以使用 `git merge origin/master` 手动合并更改。

在执行 `git pull` 命令前，考虑使用 `git fetch` 和 `git log` 或 `git diff` 来检查远程更改，确保你了解即将合并的内容。这有助于避免意外的合并冲突或丢失工作。



使用场景：当远程的仓库有新的提交，我们需要先切换到原分支（一个是原分支，一个是我从原分支 checkout 创建的个人分支），然后在原分支里面，进行 git pull origin master

![image-20240719181324797](https://raw.githubusercontent.com/ZZZRamsey/PicGo_save/main/202409171933073.png?token=AVDP3DE4QZHPSJID57NHXELG5FUUS)







**此时有我们修改的提交 f-commit，但是没有远程仓库的修改**



<img src="https://raw.githubusercontent.com/ZZZRamsey/PicGo_save/main/202409171933074.png?token=AVDP3DEHYYYBO5R2G2QVMQTG5FUUW" alt="image-20240719181347901" style="zoom: 50%;" />



git rebase main 的意思是，把我的修改先拿到一边，把远端最新的修改拿过来， 接着在这个最新的修改之上，把我的 commit 尝试弄上去，如下图。

这个过程中，可能会有 rebase conflict，如果出现了 rebase conflict，就需要手动选择，你到底要哪一段代码

rebase 成功之后，相当于是在最新的原分支上，进行了我们自己的修改，**这也是使用 rebase 而不是 merge 的好处**

<img src="https://raw.githubusercontent.com/ZZZRamsey/PicGo_save/main/202409171933075.png?token=AVDP3DEMJP2JYMVAF6I4K6TG5FUU2" alt="image-20240719181521324" style="zoom:50%;" />



### 方法二（法一的详细版，可以让你选择合并与否，合并之前可以看看差异）

要同步 Git 远程仓库的状态，同时保留本地已有的修改，可以按照以下步骤操作：

1. **检查当前分支**： 首先确认你正在正确的分支上操作。使用 `git branch` 查看所有分支，并用 `git checkout <branch>` 切换到需要同步的分支。

2. **拉取远程仓库的更新**： 使用 `git fetch` 命令来获取远程仓库的最新状态，但不立即合并任何更改。

   ```bash
   git fetch origin
   ```

3. **查看差异**： 使用 `git log` 或者 `git diff` 来查看本地分支和远程分支之间的差异。

   ```bash
   git log <branch>..origin/<branch>
   git diff <branch> origin/<branch>
   ```

4. **保留本地修改**： 如果有未提交的更改，可以暂存它们，以便稍后恢复。

   ```bash
   git stash save "Stash message"
   ```

5. **合并远程更改**： 将远程分支的最新状态合并到本地分支。这里可以选择 `merge` 或者 `rebase` 方法。

   - 使用

     ```
     git merge
     ```

     来合并远程分支的更改。

     ```bash
     git merge origin/<branch>
     ```

   - 或者使用

     ```
     git rebase
     ```

     来重新应用本地更改到远程分支的顶部。

     ```bash
     git rebase origin/<branch>
     ```

6. **解决可能的冲突**： 如果在合并过程中出现冲突，需要手动解决这些冲突。可以使用 `git status` 查看冲突的文件，并编辑这些文件来解决冲突。

7. **恢复暂存的更改**： 如果之前有暂存的更改，现在可以恢复它们。

   ```bash
   git stash pop
   ```

8. **提交更改**： 最后，提交合并后的更改。

   ```bash
   git add .
   git commit -m "Merge remote-tracking branch 'origin/<branch>' into <branch>"
   ```

9. **推送更改到远程仓库**： 如果一切顺利，可以将更改推送到远程仓库。

   ```bash
   git push origin <branch>
   ```

通过上述步骤，你可以安全地同步远程仓库的状态，同时保留本地已有的修改。这样可以避免不必要的数据丢失，并且能够有效地管理本地和远程的差异。



#### git fetch 之后会发生什么

当你执行 `git fetch` 命令时，Git 会从指定的远程仓库下载所有的更新信息，并将这些信息存储在本地仓库中，但不会自动修改你当前的工作目录或分支的历史记录。具体来说，`git fetch` 之后会发生以下几件事情：

1. **下载远程分支的提交历史**： Git 会从远程仓库下载所有新的提交记录，并将它们存储在本地的 `.git/refs/remotes/` 目录下对应的远程分支跟踪分支中。例如，如果你是从名为 `origin` 的远程仓库中获取更新，那么新的提交会被存储在类似 `.git/refs/remotes/origin/main` 的路径下。
2. **更新远程分支的引用**： Git 会更新本地仓库中对远程分支的引用，使得你可以查看远程分支的最新状态。这些引用通常被称为“远程跟踪分支”（remote-tracking branches）。
3. **不改变当前分支的 HEAD 指针**： `git fetch` <u>不会改变你当前所在分支的 HEAD 指针的位置</u>。这意味着你的工作目录和当前分支的提交历史不会被直接修改。
4. **可以查看远程分支的变化**： 取得远程分支的信息后，你<u>可以使用 `git log` 或 `git diff` 命令来查看远程分支和本地分支之间的差异。</u>
5. **为后续操作准备**： `git fetch` <u>为后续的合并或重置操作提供了基础</u>。例如，你可以选择使用 `git merge` 或 `git rebase` 来将远程分支的更改合并到你的本地分支。



总结来说，`git fetch` 主要是用来获取远程仓库的最新状态，而不对本地的工作目录或分支的历史记录进行任何修改。这是进行更复杂的 Git 操作前的一个重要步骤，比如合并远程分支的更改到本地分支。









## reset回滚到某个提交

#### 操作步骤

在 Git 中，回滚到某个特定的提交可以通过以下步骤完成：

1. **查找提交的哈希值**: 使用 `git log` 命令来查看提交历史，找到你想要回滚到的提交的哈希值。你可以使用 `--oneline` 选项使输出更加简洁。

   ```
   git log --oneline
   ```

2. **硬重置到特定提交**: 使用 `git reset --hard` 命令，后跟你从 `git log` 输出中找到的提交哈希值。这会将你的工作目录和暂存区恢复到该提交的状态，同时还会移动分支指针到该提交。

   ```
   git reset --hard <commit-hash>
   ```

   注意：这将丢失你当前分支上该提交之后的所有更改和提交。在执行此操作之前，请确保你已经保存了任何未提交的工作，或者创建了一个备份。

3. **强制推送（如果需要）**: 如果你已经将分支推送到远程仓库，并且该分支上的提交历史与远程仓库不同，你需要使用 `git push --force` 或 `git push -f` 来更新远程仓库。但是，这会覆盖远程仓库的历史，因此请谨慎操作。

   ```sh
   git push --force
   # 或者
   git push -f
   ```

   在某些情况下，远程仓库可能有保护措施防止强制推送，你可能需要联系仓库管理员去除这些保护，或者使用具有相应权限的用户身份进行推送。

**注意事项**:

- 使用 `git reset --hard` 是一个破坏性的操作，它会丢弃未提交的更改和提交历史中该提交之后的所有提交。
- 在执行 `git reset --hard` 之前，建议 **创建一个备份** 或 **打一个补丁**，以防万一需要恢复丢失的数据。
- 如果你只是想撤销一些提交，但保留工作目录的更改，可以使用 `git reset` 不带 `--hard` 选项，或者使用 **`git revert` 来创建新的提交来撤销之前的更改**。



如果误操作，也不用担心，git 中的所有操作都是可以回溯的。

	1. 使用 git reflog 命令，查看操作的历史记录。
	2. 找到误操作之前的版本号
	3. 再使用 git reset 命令来回退到这个版本就行了。



#### reset 的参数

git reset 指令参数
--soft
--hard
--mixed（默认）

--soft 和--mixed 的使用场景基本一样，一般来说，但我们连续提交了多个版本，但是又觉得这些提交没有太大意义，可以合并为一个版本的时候，就可以通过这两个参数来进行回退之后再重新提交，唯一的区别就是：
	 

	--mixed 模式要执行以下 git add 操作，将修改好的内容重新添加到暂存区。（因为暂存区被清空了）
	--soft 模式就不需要，因为 soft 模式，工作区和暂存区都不会被清空。

谨慎使用--hard，因为会删除两个版本之间工作区暂存区的所有修改内容。





## git checkout 恢复工作目录中的文件到上次提交的状态。

当你使用 `git checkout -- <file>` 命令时，你实际上是在告诉 Git 将工作目录中的文件 `<file>` 恢复到其最后一次提交的状态。这会丢弃工作目录中对这个文件的所有未暂存的更改。

具体步骤如下：

1. **确认状态**：首先使用 `git status` 查看当前工作目录中的文件状态，确认哪些文件有未暂存的更改。
2. **恢复文件**：对于每个需要恢复的文件，运行 `git checkout -- <file>` 命令。这里的 `<file>` 是文件的完整路径，例如：
   - `git checkout -- configs/inference.yaml`
3. **验证结果**：再次运行 `git status` 来确认所有指定的文件是否已经被恢复到了上次提交的状态。

如果你想要一次性恢复所有文件到上次提交的状态，可以使用通配符来匹配所有文件，例如：

- `git checkout -- .` 这个命令会恢复当前目录及其子目录下的所有文件。

请注意，这些操作会直接覆盖工作目录中的文件，所以如果你需要保留任何未提交的更改，请先进行备份或暂存这些更改。**checkout单个文件的操作不会被记录到 git reflog 中，所以不可回溯。如果不确定那个文件是否需要修改，建议暂存stash**



## 操作回溯 git reflog

如果误操作，也不用担心，git 中的所有操作都是可以回溯的。

	1. 使用 git reflog 命令，查看操作的历史记录。
	2. 找到误操作之前的版本号
	3. 再使用 git reset 命令来回退到这个版本就行了。



git reflog ：更详细的 git log --oneline 包含 commit , pull , revert , reset 等等改变分支的操作

注意：删了分支就不能 reset 回来了。



Git 的引用日志 (`reflog`) 用于记录每个引用（比如分支、标签和 HEAD）的更改历史。当您执行某些操作（如 `git checkout`、`git reset` 等）时，Git 会在 `reflog` 中留下一条记录。

默认情况下，Git 会保留 `reflog` 记录一段时间，通常是一段时间后才会自动清理旧的 `reflog` 记录。这个时间可以通过 Git 的配置变量 `gc.reflogExpire` 来设置，<u>默认值通常是 30 天</u>。这意味着如果没有其他操作，`reflog` 中的条目将在大约一个月后被自动删除。

如果您想查看或更改这个设置，可以使用以下命令：

```sh
# 查看当前设置
git config --get gc.reflogExpire

# 设置新的过期时间（单位是秒，也可以使用更友好的格式，如 90.days）
git config --global gc.reflogExpire 90.days
```

此外，`reflog` 的清理是由 `git gc` 命令触发的，这个命令除了清理 `reflog` 外，还会进行其他优化操作，如合并重复的对象、释放未引用的对象等。`git gc` 通常由 Git 自动调用，但您也可以手动运行它来立即清理 `reflog`。

请注意，即使 `reflog` 中的记录被清理了，Git 也会保留那些已经被至少一个引用指向的对象，以防止丢失重要的数据。因此，即使 `reflog` 清理了某个提交的记录，只要该提交仍然可以通过其他引用访问，它就不会被删除。





## git revert

在 Git 中，`revert` 是一种用于撤销先前提交更改的方式，但它不会删除任何提交，而是通过创建一个新的提交来“反转”旧提交的效果。这种方法保留了项目的历史完整性，因为原始的提交仍然存在，只是其效果被后来的提交抵消了。

#### 如何使用 `git revert`

1. **确定要撤销的提交**: 使用 `git log` 查找你想要撤销的提交的哈希值。

   ```sh
   git log --oneline
   ```

2. **创建一个 revert 提交**: 使用 `git revert` 命令，后跟你想要撤销的提交的哈希值。这将自动创建一个新的提交，其效果正好与原提交相反。

   ```
   git revert <commit-hash>
   ```

   这个命令会打开一个文本编辑器，让你有机会修改提交消息。默认的提交消息会包含 “Revert” 字样以及被撤销提交的完整消息。

3. **解决冲突（如果有的话）**: 如果被撤销的提交与之后的提交之间有冲突，`git revert` 会暂停并要求你手动解决冲突。解决完冲突后，使用 `git add` 添加解决后的文件，然后继续 `revert` 过程。

   ```
   git add <conflicted-file>
   git revert --continue
   ```

4. **推送 revert 提交**: 将 revert 提交推送到远程仓库。由于这会改变远程仓库的历史，你可能需要使用 `--force-with-lease` 或者 `--force` 选项，但这取决于远程仓库的配置。

   ```
   git push origin HEAD
   # 或者使用 force push
   git push origin HEAD --force-with-lease
   ```

#### 优点

- **保留历史**: `revert` 保留了项目的完整历史记录，这对于追溯错误原因和审计非常有用。
- **易于理解**: 新的 revert 提交清晰地表明了某次更改已被撤销，这有助于其他贡献者理解项目的演变过程。

#### 注意事项

- 在执行 `git revert` 之前，确保你和其他团队成员都清楚这一操作的目的和影响。
- 如果你在一个公共分支上执行 `revert`，并且该分支已经被其他人克隆或拉取，你需要通知他们有关的更改。





#### 输出

```bash
b5bab0a (HEAD -> test1, zls-feature2-sku-recognition-pytorch) HEAD@{0}: checkout: moving from test2 to test1		# 这是我当前的分支
0f02774 HEAD@{1}: commit: Revert "add debugger in gunicorn_conf.py"		#这是我在已删除分支上的一次提交
```

在 `git reflog` 的输出中，`HEAD@{1}` 指的是最近的第二个状态，即从当前 HEAD 的前一个状态。这里的数字 `1` 表示这是相对于当前 HEAD 的前一次更新。

`git reflog` 列出了所有对引用（如 HEAD）的操作历史。每当 HEAD 或其他引用发生变化，比如通过 `commit`, `checkout`, `reset`, `merge` 等命令，reflog 就会记录这个变化。`HEAD@{0}` 总是指向当前 HEAD 的状态，而 `HEAD@{1}` 则是上一次的状态，依此类推。

所以，在你给出的例子中：

- `b5bab0a (HEAD -> test1, zls-feature2-sku-recognition-pytorch) HEAD@{0}: checkout: moving from test2 to test1` 这一行表示的是最近的一次操作，也就是从分支 `test2` 切换到了 `test1` 分支。
- `0f02774 HEAD@{1}: commit: Revert "add debugger in gunicorn_conf.py"` 这一行表示的是在切换分支之前的一次提交，这次提交的内容是撤销了在 `gunicorn_conf.py` 文件中添加调试器的改动。

如果你想要回到 `HEAD@{1}` 的状态，你可以使用 `git reset` 命令，具体如下：

```
git reset --hard HEAD@{1}
```

这将会把你的工作树和索引重置到 **`HEAD@{1}` 所指向的提交状态**（并不会把删除的分支重新创建回来）。请注意，这样做会丢弃自那次提交以来所做的任何更改，所以在执行这样的操作之前一定要小心，确保你不会丢失任何重要的工作。





## git clone 时保存账号密码到本地

- **清除已保存的凭据**：

  ```sh
  git config --global --unset credential.helper
  ```


保存 git clone 账号密码
```sh
# 设置Git的凭据存储方式为store（长期存储）
git config --global credential.helper store

# 构建并执行git clone命令
# 注意：这里使用了http方式，你需要将<username>和<password>替换为实际的用户名和密码
# 以及将<git-url>替换为实际的Git仓库URL
git clone http://<username>:<password>@<git-url>/$name.git

# 如果你想使用HTTPS协议，URL看起来应该是这样的：
# git clone https://<username>:<password>@github.com/<username>/<reponame>.git
```
在上面的脚本中，git config --global credential.helper store 这行代码设置了 Git 全局的凭据存储方式为 store，这意味着 Git 会记住你的用户名和密码，直到你手动清除它们。

请注意，直接在脚本中硬编码密码是不安全的，因此在这个例子中，我使用了占位符 <username> 和 <password> 以及 <git-url>。在实际使用中，你应该将这些占位符替换为实际的值。

另外，如果你的 Git 服务器要求使用 HTTPS 协议，你需要将 URL 中的 http://替换成 https://，并且确保你的用户名和密码是正确的。



## git 提交时使用 Vim 作为默认的编辑器

要在 Git 提交时使用 Vim 作为默认的编辑器，你可以按照以下步骤进行配置：

1. **设置 Git 编辑器** 打开终端或命令行工具，输入以下命令来设置 Git 使用 Vim 作为默认编辑器：

   ```bash
   git config --global core.editor "vim"
   ```

2. **验证配置** 检查你的设置是否生效，可以通过下面的命令查看当前的编辑器配置：

   ```bash
   git config --get core.editor
   ```

   如果输出结果是 `vim`，那么你就已经成功地将 Vim 设置为 Git 的默认编辑器了。

3. **进行 Git 提交** 当你执行 `git commit` 或者 `git commit -a` 命令时，Vim 将会被自动调用以编辑提交信息。在 Vim 中，你可以使用以下基本命令进行操作：

   - 按下 `i` 键进入插入模式，开始编辑提交信息。
   - 编辑完成后，按下 `Esc` 键退出插入模式。
   - 接着输入 `:wq` 并按回车键保存并退出 Vim。
   - 或者，你也可以输入 `:x` 直接保存并退出。
   - 如果你只想退出不保存，可以输入 `:q!`。

4. **使用 Vim 插件** 如果你经常使用 Vim 编辑 Git 提交信息，可以考虑安装一些 Vim 插件来增强 Git 功能，例如 `gitgutter` 或 `fugitive.vim`，这些插件可以提供更丰富的 Git 集成体验。

完成以上步骤后，每次进行 Git 提交时，Vim 编辑器就会自动启动，供你编辑提交信息。





## 查看 git 的配置文件

#### --global的含义

在Git中，`git config --global --edit` 命令中的 `--global` 选项指的是当前用户的所有文件的配置。当你使用 `--global` 选项时，Git会编辑或创建位于用户主目录下的 `.gitconfig` 文件。这个文件包含了适用于该用户所有Git仓库的配置选项。

如果你想要编辑特定仓库的配置，而不是全局配置，你可以在仓库目录内运行 `git config --edit` 命令，不带 `--global` 选项。这将编辑或创建该仓库下的 `.git/config` 文件，其中的配置选项仅适用于当前仓库。

总结来说，`--global` 指的是当前用户的全局配置，适用于该用户的所有Git仓库。如果你想要编辑特定仓库的配置，请在该仓库目录内运行不带 `--global` 选项的 `git config --edit` 命令。





问：当我修改了 git 的默认编辑器为 vim，如何保存此设置

当你使用 `git config` 命令来修改 Git 的默认编辑器为 Vim 时，设置会立即生效。但是，为了确保这个设置被永久保存，你需要将这个配置添加到你的 Git 配置文件中，通常是 `~/.gitconfig` 文件（对于 Unix-like 系统）或 `%USERPROFILE%\.gitconfig` 或 `%USERPROFILE%\_gitconfig`（对于 Windows 系统）。



#### 查看配置

如果你之前已经使用 `git config` 命令进行了设置，那么这个设置应该已经被自动添加到了你的 Git 配置文件中。你可以通过以下命令来检查是否已经正确设置：

```sh
git config --global --get core.editor
```

这应该会返回 `vim` 或者是你的完整路径，比如 `/usr/bin/vim`。



#### 打开配置文件

如果你想手动确认或编辑这个配置文件，可以使用以下命令打开它：

```sh
# 对于Unix-like系统
$ git config --global --edit

# 对于Windows系统
> git config --global --edit
```

这将使用你的默认编辑器（在这里应该是 Vim）打开 `.gitconfig` 文件，你可以在这里查看或修改设置。

如果你希望确保 Vim 被设置为默认编辑器，并且这个设置被持久化，你可以直接在 `.gitconfig` 文件中添加或修改以下行：

```ini
[core]
    editor = vim
```

保存并关闭文件后，这个设置就会被永久保存，每次你使用 Git 需要编辑器时，Vim 就会被调用。





如果你想要查看当前的配置信息，可以使用：

```shell
git config --list
```

这条命令会列出所有的配置项及其值。

请注意，如果你已经为特定仓库设置了局部配置，那么局部配置会覆盖全局配置。如果你希望某个特定仓库使用不同的配置，可以在该仓库目录下创建一个`.git/config`文件，并直接编辑这个文件或者使用`git config`命令来设置局部配置。例如：

```shell
cd /path/to/your/repo
git config user.name "Your Name"
git config user.email "youremail@example.com"
```



这样设置的配置仅对该仓库有效。

## git 分支改名

在 Git 中，你可以使用以下步骤来更改本地分支的名称，并随后更新远程分支的名称：

#### 更改本地分支名称

1. 首先确认你正在使用的分支，或者切换到你要改名的分支：

   ```sh
   git checkout <old-branch-name>
   ```

2. 使用 `git branch -m` 命令来修改分支名称：

   ```sh
   git branch -m <new-branch-name>
   ```

#### 更新远程分支名称

1. 删除远程仓库中的旧分支名称：

   ```sh
   git push origin --delete <old-branch-name>
   ```

2. 将新的分支名称推送到远程仓库：

   ```sh
   git push origin <new-branch-name>
   ```

这样，你不仅更改了本地分支的名称，同时也更新了远程仓库中的分支名称。



## 查看分支结构图

要查看当前本地仓库的分支结构图，你可以使用 `git log` 命令结合一些选项来生成一个文本形式的分支图。这里是一个常用的命令组合：

```
git log --graph --oneline --decorate --all
```

这个命令的含义如下：

- `--graph`: 在输出中添加 ASCII 图形表示法，显示分支的合并历史。
- `--oneline`: 将每个提交压缩成一行，使输出更加紧凑。
- `--decorate`: 在每个提交前加上标签和分支引用，帮助你识别每个提交所属的分支。
- `--all`: 显示所有分支的历史记录，包括合并进来的分支。

#### 示例命令

```
git log --graph --oneline --decorate --all
```

这条命令会生成一个文本形式的分支图，其中包含了所有分支的合并历史，并以 ASCII 图形表示法显示分支的合并点，同时每个提交会被压缩成一行，并且每个提交前会有标签和分支引用的信息。

#### 输出示例

假设你的仓库中有如下提交历史：

```
* commit-hash (HEAD -> master, origin/master, origin/HEAD)
|\
| * commit-hash (feature-branch)
* | commit-hash
|/
* commit-hash
```

在这个例子中，“master”分支与“feature-branch”分支有一个共同的祖先提交，并且“master”分支已经合并了“feature-branch”。

#### 可选的其他选项

- `--simplify-by-decoration`: 这个选项可以帮助简化图形输出，只显示那些被标签或分支引用的提交。
- `--simplify-merges`: 这个选项可以帮助进一步简化图形输出，去除不必要的合并点。

例如，你可以使用这些选项来进一步优化输出：

```
git log --graph --oneline --decorate --all --simplify-by-decoration --simplify-merges
```

这将会生成一个更简洁的分支图。

#### 使用图形化工具

如果你希望使用图形化工具查看分支图，可以考虑使用 Git 的图形化客户端，如 GitKraken、SourceTree 或 Git Extensions 等。这些工具提供了直观的界面，可以轻松地查看和管理分支。
