## Linux 查看系统版本信息

```sh
hostnamectl
```



要查看 Linux 版本信息，可以使用以下命令：

### `lsb_release` 命令

```
lsb_release -a
```

这个命令将显示发行版的详细信息，包括发行版名称、版本号、代号等。

###  `cat` 命令读取 `/etc/os-release` 文件

```
cat /etc/os-release
```

这个命令将显示系统的发行版信息，包括名称、版本号和其他相关信息。

###  `uname` 命令

```
uname -a
```

这个命令将显示系统的内核版本和一些其他信息。

### `hostnamectl` 命令

```
hostnamectl
```

这个命令也可以显示操作系统和内核的版本信息。

### 示例输出

#### 使用 `lsb_release -a`

```
$ lsb_release -a
No LSB modules are available.
Distributor ID: Ubuntu
Description:    Ubuntu 20.04.4 LTS
Release:        20.04
Codename:       focal
```

#### 使用 `cat /etc/os-release`

```
$ cat /etc/os-release
NAME="Ubuntu"
VERSION="20.04.4 LTS (Focal Fossa)"
ID=ubuntu
ID_LIKE=debian
PRETTY_NAME="Ubuntu 20.04.4 LTS"
VERSION_ID="20.04"
HOME_URL="https://www.ubuntu.com/"
SUPPORT_URL="https://help.ubuntu.com/"
BUG_REPORT_URL="https://bugs.launchpad.net/ubuntu/"
PRIVACY_POLICY_URL="https://www.ubuntu.com/legal/terms-and-policies/privacy-policy"
VERSION_CODENAME=focal
UBUNTU_CODENAME=focal
```

#### 使用 `uname -a`

```
$ uname -a
Linux hostname 5.4.0-104-generic #118-Ubuntu SMP Fri Feb 5 11:44:42 UTC 2021 x86_64 x86_64 x86_64 GNU/Linux
```

#### 使用 `hostnamectl`

```
$ hostnamectl
   Static hostname: hostname
         Icon name: computer-vm
           Chassis: vm
        Machine ID: ***************
           Boot ID: ***************
    Virtualization: kvm
  Operating System: Ubuntu 20.04.4 LTS
            Kernel: Linux 5.4.0-104-generic
      Architecture: x86-64
```

选择你喜欢的命令来查看 Linux 版本信息。不同的命令会提供不同的详细信息，这些信息对于了解系统的发行版和版本非常有用。



![image-20230310171036914](C:\Users\lenovo\AppData\Roaming\Typora\typora-user-images\image-20230310171036914.png)

终端内赋值 ctrl insert，shift insert

[Linux 基础命令（三）文件的移动、删除、复制 详细_将/mnt 下文件 hello.txt 文件移动到/tmp 下-CSDN 博客](https://blog.csdn.net/qq_52734656/article/details/119479780)



## 文件的创建

touch 命令用于修改文件或者目录的时间属性，包括存取时间和更改时间。若文件不存在，系统会建立一个新的文件。

[Linux touch 命令 | 菜鸟教程 (runoob.com)](https://www.runoob.com/linux/linux-comm-touch.html)



### 使用 `touch` 命令

`touch` 命令用于创建一个空文件，或者更新现有文件的访问和修改时间。

```sh
touch filename
```

例如，创建一个名为 `example.txt` 的空文件：

```sh
touch example.txt
```



### 使用 `echo` 命令

`echo` 命令可以将文本输出到一个文件中。如果文件不存在，它将被创建；如果文件存在，内容将被覆盖。

```sh
echo "some text" > filename
```

例如，创建一个名为 `example.txt` 的文件，并写入 "Hello, World!"：

```sh
echo "Hello, World!" > example.txt
```



## 文件的移动、删除与复制

###         mv

命令格式

**mv \[选项\] 源文件  目标位置**

```bash
mv move [移动 改名]

Rename SOURCE to DEST, or move SOURCE(s) to DIRECTORY.

把目标文件[SRC]移动到目标位置[DEST]改名，或者把源文件移动到目标目录

1.移动
#mv a.txt /tmp  //把文件a.txt移动到/tmp 目录下

2.改名
#mv a.txt aa.txt  //把文件a.txt移动到当前目录下并改名为aa.txt
#mv /tmp/a.txt  aaa.txt  //把/tmp目录下的a.txt文件移动到当前目录下并改名为aaa.txt

在linux系统中 如果文件前面不加路径 默认为当前路径下的文件

3.对多个文件移动
#mv file1.txt file2.txt file3.txt  /tmp //把当前目录下的file{1..5}.txt 文件移动到/tmp目录下

mv命令默认最后一个参数为目标位置 其余的为源文件

4.对多个文件和目录文件进行移动
#mv /tmp/file1.txt /tmp/file2.txt /tmp/dir1  /root
#把/tmp目录下的file1.txt file2.txt dir1 移动到/root目录下
#移动目录时  如果目录里面有文件 目录下的文件也会一起移动 
```

**mv file1  /~   当目标目录不存在时，文件被移动到/目录下，更名为~**

当在/目录下查看~文件时，vi ~  结果看到空白，是因为文件最末尾是空白的，导致误认为不是目标文件，找了半天，好醉，最后使用 gedit 查看后发现就是目标文件





### rsync

#### 示例目录结构

```
markdown复制代码source/
  ├── dir1/
  │   └── file1.txt
  └── dir2/
      └── file2.txt

destination/
  ├── dir1/
  │   └── file3.txt
  └── dir3/
      └── file4.txt
```

你希望移动后 `destination` 的结构如下：

```
markdown复制代码destination/
  ├── dir1/
  │   ├── file1.txt
  │   └── file3.txt
  ├── dir2/
  │   └── file2.txt
  └── dir3/
      └── file4.txt
```

**步骤 1：使用 `rsync` 命令**

`rsync` 是一个功能强大的工具，可以用于同步文件和文件夹。它可以很好地处理合并同名文件夹的情况。

```
rsync -av --progress source/ destination/
```

- `-a`：归档模式，表示递归复制并保持所有属性。
- `-v`：详细输出模式，显示正在处理的文件。
- `--progress`：显示进度信息。

- `-z`：用于启用压缩，其全称是 `--compress`



当使用 `-z` 参数时，`rsync` 会在数据传输过程中对数据进行压缩，这可以显著减少网络带宽的使用，尤其是在传输大量小文件或者数据本身未被压缩的情况下效果更明显。

压缩在发送端进行，解压缩在接收端完成，这样可以减少在网络上传输的数据量，从而加快传输速度，尤其是在低带宽或高延迟的网络环境中。但是，压缩和解压缩过程会消耗更多的 CPU 资源，因此，在 CPU 性能有限的系统上，这种压缩可能会导致整体传输速度变慢。



压缩级别：

默认情况下，`rsync` 使用中等的压缩级别。如果需要调整压缩级别，可以使用 `--compress-level=N` 选项，其中 `N` 是一个介于 0 到 9 之间的整数，0 表示无压缩，数值越大压缩程度越高，但也会消耗更多的 CPU 资源。

例如，要使用最高的压缩级别 9，可以这样设置：

```bash
rsync -av --compress-level=9 source_directory/ destination_directory/
```



**步骤 2：删除源文件夹**

在确认所有文件已成功移动并合并后，你可以删除源文件夹。

```
rm -rf source/
```









## rsync 自动判断是否存在重复文件，进行传输

```sh
 rsync -avzu --partial --progress /home/data03/zls/lszhu24/MagicDrive/pretrained lird22@172.16.46.207:/home/data/lszhu24/MagicDrive/MagicDrive/
```



<u> **注意，要传输的文件夹如果最后加上 `/` 那么传输的就是文件夹里面的内容，不包括文件夹，如果你想要传文件夹，则要这样写 `MagicDrive/pretained`** </u>



## rsync 给远程服务器同步文件

如果你想使用 `scp` 或者 `rsync` 来完成这个任务，你可以按照下面的方法操作。

### 对比 `scp` 

`scp` 命令主要用于安全地复制文件或目录，但它并不支持排除子目录的功能。因此，如果你只能使用 `scp` 并且需要排除子目录，你可能需要手动列出所有的文件并排除子目录。

由于 `scp` 不支持排除子目录，这里就不详细说明了。通常情况下，我们推荐使用 `rsync`，因为它提供了更灵活的选项来排除文件和目录。

### 使用 `rsync` 的方法

`rsync` 是一个非常强大的工具，可以用来同步文件夹，并且支持排除子目录。你可以使用 `--exclude` 选项来排除子目录。

#### 步骤 1: 连接到远程服务器

首先，你需要通过 SSH 连接到远程服务器，或者直接在命令行中使用 `rsync` 命令。

#### 步骤 2: 使用 `rsync` 同步文件

为了排除每个子目录，你可以使用 `--exclude` 选项多次，并指定每个子目录的名称。但更好的方式是使用 `--exclude='/*/'` 来排除所有子目录。

#### 步骤 3: 检查本地文件是否存在

你可以使用 `--update` 选项来确保只有当远程文件比本地文件新时才进行传输。

#### 示例命令

假设远程服务器上的文件夹为 `/remote/folder`，并且你想将这个文件夹的内容同步到本地的 `/local/folder`，你可以使用如下的 `rsync` 命令：

```
rsync -avz --update --exclude='/*/' user@remote-server:/remote/folder/ /local/folder/
```

这里的选项含义如下：

- `-a` 表示归档模式，保持文件属性不变。
- `-v` 表示详细模式，输出详细信息。
- `-z` 表示启用压缩，加快传输速度。
- `-P` 显示传输进度
- `--update` 只更新那些已经改变的文件。也可以写成-u
- `--exclude='/*/'` 排除所有子目录。
- `--partial`：保留部分传输的文件。如果传输中断，下次继续传输时可以从断点处继续，而不是重新开始。

### 注意事项

- 确保你有远程服务器的访问权限。
- 确保 `/local/folder` 已经存在，否则 `rsync` 将会创建它。
- 如果 `/remote/folder` 中有多个级别的子目录，`--exclude='/*/'` 可能不会按预期工作，因为它只排除一级子目录。在这种情况下，你可能需要使用更复杂的排除规则或者正则表达式。

### 示例

如果你的远程服务器上有多个层级的子目录，并且你想排除所有这些子目录，你可以尝试使用更复杂的排除规则，例如：

```
rsync -avz --update --exclude='*/' user@remote-server:/remote/folder/ /local/folder/
```

这里 `--exclude='*/'` 会排除所有子目录。请注意，这种方法可能会排除所有以斜杠结尾的条目，包括文件，所以请根据实际情况调整排除规则。





### mv 和 rsync 的对比

**使用 `mv` 命令直接移动**

如果你使用 `mv` 命令直接移动文件夹，注意它不会自动合并同名文件夹，而是会覆盖同名文件夹：

```
mv source/* destination/
```

==这种方法在同名文件夹存在时会导致覆盖，丢失原有文件==，因此并不推荐用于需要合并同名文件夹的情况。





### 使用 rsync 移动文件

为了移动文件，你可以使用 `--remove-source-files` 或 `-u` 和 `--delete-after` 选项。`--remove-source-files` 选项会在文件被成功同步到目的地后，从源位置删除文件。`-u` 选项确保只有当源文件比目标文件新或目标文件不存在时才进行更新，而 `--delete-after` 则在同步完成后删除目标目录中多余的文件。

示例：

如果你想将 `/source/path` 下的文件移动到 `/destination/path`，可以使用以下命令：

```bash
rsync -avP --remove-source-files /source/path/ /destination/path/
```

这里，`-a` 表示归档模式，它保留符号链接、文件权限、用户和组所有权、时间戳等；`-v` 表示详细模式，它会显示详细的同步信息。

如果你想要在移动文件的同时保持目标目录的整洁，删除目标目录中不再存在于源目录的文件，可以使用：

```bash
rsync -avu --delete-after /source/path/ /destination/path/
```

在这个例子中，`-u` 确保只有在需要时才更新文件，而 `--delete-after` 在同步完成后删除目标目录中多余的文件。

需要注意的是，`rsync` 不会移动空目录，除非你明确指定了 `--dirs` 选项。因此，如果你想要移动目录结构，即使目录为空，也应该包含这个选项。

最后，一定要小心使用 `rsync` 的删除功能，因为它可能会永久删除文件。在使用 `--delete` 或 `--delete-after` 选项之前，最好确认你的命令正确无误，并且你已经备份了任何可能需要的数据。





### 使用 rsync 复制时排除某些文件

当你使用 `rsync` 命令进行文件或目录的复制时，你可能会想要排除一些特定的文件或目录，以避免不必要的数据传输或存储空间占用。`rsync` 提供了多种方式来排除文件或目录：

#### 基本排除选项

- `--exclude=PATTERN`: 排除符合指定模式的文件或目录。
- `--exclude-from=FILE`: 从指定的文件中读取排除模式列表。



```bash
rsync -avz \
    --exclude='*.tmp' \
    --exclude='logs/' \
    source_directory/ destination_directory/
```

在这个例子中，`rsync` 会复制 `source_directory` 的内容到 `destination_directory`，但会排除所有 `.tmp` 扩展名的文件和 `logs/` 目录。

#### 更复杂的排除规则

如果你想使用更复杂的排除规则，可以创建一个包含多个排除模式的文件，然后使用 `--exclude-from` 选项指向这个文件。

##### 示例排除文件（假设名为 `exclude_patterns`）：

```txt
# 注释行以#开始
# 排除所有.log文件
*.log
# 排除所有以~结尾的文件（通常是备份文件）
*~
# 排除所有Thumbs.db文件（Windows系统的缩略图缓存）
Thumbs.db
# 排除所有隐藏的临时文件（以.开头）
.*~
```

然后执行：

```bash
rsync -avz \
    --exclude-from=exclude_patterns \
    source_directory/ destination_directory/
```



Tips:

- `rsync` 的排除模式遵循特定的语法，包括正则表达式和 globbing 模式。
- 如果你想在复制时删除目标目录中不再存在于源目录中的文件或目录，可以添加 `--delete` 选项。
- 当使用 `--exclude` 或 `--exclude-from` 时，确保模式正确匹配你想要排除的文件或目录，以避免意外的数据丢失。



### 文件的删除

####         命令格式

​            **rm  \[选项\]  目标文件**

```bash
rm remove 删除

Remove (unlink) the FILE(s).

删除（解除）文件

常用的rm命令参数：

-f force ignore nonexistent files and arguments, never prompt 忽略不存在的文件和参数，不提示

rm -f filename 删除文件且不询问

-r or -R recursive remove directories and their contents recursively 递归地删除目录及其内容

rm -rf dirname 删除目录且不询问

常用命令

rm -rf ./* 删除当前目录下的所有文件

注：删除时谨慎使用* 不要把根目录全删了
```





### 文件的复制

####         命令格式

​            **cp  \[选项\]  源文件  目标位置**

```bash
cp copy 复制

Copy SOURCE to DEST, or multiple SOURCE(s) to DIRECTORY.

把源文件[src]复制到目标位置dest，或者将多个源文件复制到目标位置

常用的cp命令参数：

-f force 与rm命令参数中的-f一致 强制删除 不询问

-r recursive 递归

复制单个文件

cp a.txt /tmp // 将当前目录下的a.txt文件复制到目录 /tmp 下

复制多个文件

cp file1.txt file2.txt file3.txt /tmp
#将多个文件复制到/tmp目录下 cp与mv命令相似 默认把最后一个参数作为目标位置 其余为源文件

复制目录

cp -r dir1 /tmp //复制目录dir1 到 /tmp下

cp -rf dir1 /tmp

cp -rf dir1/* /tmp // 复制目录dir1下的所有文件和目录到/tmp下
```



## 查看文件信息

###  使用 `ls` 和 `wc` 命令

- 查看文件数量

你可以使用 `ls` 命令列出目录中的文件，再通过 `wc -l` 命令统计行数，即文件数量：

```
ls -1 | wc -l
```

其中 `-1` 选项确保每个文件名都在单独一行。



- 查看各个文件信息

可以使用 `ls` 命令来列出文件夹中各个文件的信息。以下是一些常用的 `ls` 命令参数：

`-l`：以长格式显示文件信息，包括文件权限、所有者、大小、修改时间等。

`-a`：显示所有文件，包括以点号开头的隐藏文件。

`-h`：以人类可读的格式显示文件大小，如 MB、GB。

`-t`：按修改时间排序，最新的文件会显示在最前面。

`-r`：按相反的顺序显示文件和目录。

`-d`：只展示文件夹。



例如，要以长格式显示当前目录下的所有文件，包括隐藏文件，可以使用以下命令：

```sh
ls -la
```

tip：ls 仅限文件，不能计算文件夹大小





命令：`ls -l` 		简写：`ll`

（其中 `-1` 选项确保每个文件名都在单独一行。）



在 Linux 系统中，`ls -l` 命令用于以详细格式（长格式）列出目录内容。让我们逐行解释这个命令的输出：

```shell
total 204
-rw-rw-r-- 1 lird22 lird22 206882 5月  16 18:05 legend.png
```

#### ls 输出解释

1. **`total 204`**:
   - 这个部分表示当前目录中所有文件大小的总和，单位是块（block）。块的大小通常是 512 字节，可以根据文件系统的不同有所变化。
2. **`-rw-rw-r--`**:
   - 这是文件的权限字符串，由 10 个字符组成。
     - 第一个字符 `-` 表示这是一个普通文件（`d` 表示目录，`l` 表示符号链接，等等）。
     - 接下来的三个字符 `rw-` 表示文件所有者的权限：读（r），写（w），无执行（-）。
     - 再接下

来的三个字符 `rw-` 表示文件所属组的权限：读（r），写（w），无执行（-）。 - 最后三个字符 `r--` 表示其他用户的权限：读（r），无写（-），无执行（-）。

1. **`1`**:
   
   - 表示硬链接的数量。这里显示为 1，意味着只有一个文件名指向该文件。
   
2. **`lird22`**:
   
   - 表示文件的所有者，即 `lird22` 用户。
   
3. **`lird22`**:
   
   - 表示文件的所属组，即 `lird22` 组。
   
4. **`206882`**:
   
   - 表示文件的大小，单位是字节（bytes）。这里文件大小为 206,882 字节。
   
5. **`5月 16 18:05`**:
   - 表示文件的最后修改时间。这里的时间格式是：月 日 时: 分。
   - `5月` 表示 5 月。
   - `16` 表示 16 日。
   - `18:05` 表示时间为 18:05。
   
6. **`legend.png`**:
   - 这是文件的名称。
   
     

**总结：**

该输出告诉我们，在当前目录中有一个名为 `legend.png` 的文件，其大小为 206,882 字节。文件由用户 `lird22` 拥有，并且该用户以及属于 `lird22` 组的用户对该文件具有读写权限，其他用户只能读取该文件。文件最后一次修改时间是 5 月 16 日 18:05。

如果你有更多文件或目录，这个命令会依次列出它们的详细信息。



#### du 指令

要显示文件夹占用的大小，你可以使用 `du` 命令。以下是一些常用的 `du` 命令参数：



- `-h`：以人类可读的格式显示文件夹大小，如 MB、GB。
- `-s`：仅显示汇总信息，即只显示目标文件夹的总大小，而不会列出子文件夹的大小。
- `-c`：显示总计信息，包括所有列出的文件夹的总大小。
- `--exclude=PATTERN`：排除与 `PATTERN` 匹配的文件和目录。

例如，要显示当前目录下所有文件夹的总大小，可以使用以下命令：

```sh
du -h -s *
```

这将显示当前目录下每个文件夹的总大小，并以人类可读的格式显示。





### 使用 `find` 命令找文件

`find` 命令可以递归地查找目录中的所有文件并进行计数：

```sh
find . -type f | wc -l
```

这条命令会统计当前目录及其子目录中的所有文件数量。

如果你只想统计当前目录中的文件（不包括子目录），可以使用：

```sh
find . -maxdepth 1 -type f | wc -l
```









#### 使用 `find` 命令（寻找数据集）

`find` 命令会在指定的目录及其子目录中查找满足条件的文件或目录。如果你不知道 `nuscenes` 文件夹可能位于哪个位置，可以从根目录开始搜索，但这样可能会比较慢。通常，从用户的家目录或者已知的起始点开始搜索更为高效。

```bash
find / -type d -name "nuscenes"
```

这条命令的含义是：

- `/` 表示从根目录开始搜索。
- `-type d` 指定查找的是目录（directory）。
- `-name "nuscenes"` 指定了要查找的目录名称。

#### 使用 `locate` 命令

`locate` 命令利用预先构建的文件索引数据库来快速定位文件和目录，因此它的搜索速度比 `find` 快得多，但是索引数据库可能不是实时更新的，所以在新创建的文件或目录可能找不到。

在使用 `locate` 之前，确保已安装该命令并且索引数据库是最新的。如果不确定，可以运行 `sudo updatedb` 来更新数据库，但这需要管理员权限。

```bash
locate nuscenes
```

这条命令会列出所有名为 `nuscenes` 的条目，包括文件和目录。

#### 注意事项

- 使用 `find` 命令时，由于是从根目录开始搜索，这可能需要较长时间，尤其是磁盘上的文件和目录非常多的时候。
- 对于 `locate` 命令，考虑到安全和性能问题，不建议在生产环境中以 root 用户身份直接执行全局搜索，除非确实需要这样做，并且了解其后果。

根据实际情况选择合适的命令进行搜索。





## 存储空间情况

1. 使用 `df` 命令可以显示文件系统的磁盘使用情况：

   ```
   df -h
   ```

   这个命令将会以人类可读的格式显示文件系统的磁盘使用情况，包括已用空间、可用空间、使用率等信息。

   

2. 使用 `du` 命令可以查看指定目录的磁盘使用情况：

   ```
   du -h /path/to/directory
   ```

   这个命令将会显示指定目录以及其子目录的磁盘使用情况，以人类可读的格式展示每个目录的磁盘占用情况。

   

3. 当你使用 `ls -lh .` 命令来查看当前目录下文件和子文件夹的大小时，可能会注意到子文件夹显示的大小并不是该文件夹内所有文件大小的总和。这是因为 `ls` 命令显示的文件夹大小实际上是该文件夹自身作为一个目录条目的大小，而非其包含文件的总大小。

   在大多数文件系统中，文件夹（目录）本身占用的空间很小，因为它主要存储文件名、inode 号码、权限等元数据信息，而不直接包括其内容大小。因此，当你看到所有文件夹大小相同（比如通常显示为 4.0K），这通常反映了目录条目的固定开销，而不是实际包含文件的数据量。

   如果你想查看文件夹下所有文件（包括子文件夹中的文件）的总大小，你应该使用 `du` 命令，比如：

   ```
   du -sh .
   ```

   这里的 `-s` 表示汇总（summary），只显示总计大小；`-h` 表示以人类可读的格式（如 KB, MB, GB）显示大小。这条命令会递归计算并显示当前目录及其子目录下所有文件的总大小。

   如果你只想看各级目录的大小，不包括子目录中的文件，可以使用：

   ```
   du -sh */
   ```

   这将显示当前目录下各个子目录的大小，每个目录一行，不包括子目录内部的文件大小。

`--max-depth=1` 最多往下遍历一层



## 文件压缩

zip 和 tar 只是两种不同的压缩格式



### .tar 文件

`.tar` 文件（Tape Archive）是一个归档文件，用于将多个文件和目录打包成一个单一文件，但不进行压缩。它常用于备份和传输文件。创建 `.tar` 文件的命令是 `tar`，常用的选项包括：

- `c`：创建一个新的归档文件。
- `v`：显示处理的文件。
- `f`：指定归档文件名。
- `x`：解压一个归档文件。

#### 创建 .tar 文件

```sh
tar cvf archive.tar /path/to/directory_or_files
```



#### 打包多个文件和目录

假设你有以下文件和目录：

- `file1.txt`
- `file2.txt`
- `dir1/`

你可以使用以下命令将它们打包成一个 `.tar` 文件：

```sh
tar cvf archive.tar file1.txt file2.txt dir1/
```





### .tar.gz 文件

`.tar.gz` 文件是一个使用 Gzip 压缩算法压缩的 `.tar` 文件。它先通过 `tar` 命令将多个文件和目录打包成一个 `.tar` 文件，然后再通过 `gzip` 命令进行压缩，生成 `.tar.gz` 文件。这样可以减少文件大小，更适合传输，解压的时候也要加个 z。

- **`z`：表示使用 gzip 压缩。**

#### 创建 .tar.gz 文件

```sh
tar czvf archive.tar.gz /path/to/directory_or_files
```

#### 解压 .tar.gz 文件

```sh
tar xzvf archive.tar.gz
```



#### 总结

- **.tar 文件**：只是简单的文件打包，不进行压缩。
- **.tar.gz 文件**：先打包后压缩，文件更小。





###  .zip 文件

你可以使用 `zip` 命令来创建 `.zip` 文件。常用的选项包括：

- `r`：递归处理目录，将目录中的所有文件和子目录添加到 `.zip` 文件中。
- `-e`：加密 `.zip` 文件，需要密码来解压。

#### 创建一个 .zip 文件

假设你有一个目录 `myfolder`，你想将其压缩成一个名为 `archive.zip` 的文件：

```sh
zip -r archive.zip myfolder
```

- `-r`：递归处理，将 `myfolder` 目录及其所有内容打包到 `archive.zip` 中。



#### 创建一个加密的 .zip 文件

如果你想创建一个加密的 `.zip` 文件，可以使用 `-e` 选项：

```sh
zip -re archive.zip myfolder
```

- `-r`：递归处理。
- `-e`：加密 `.zip` 文件，系统会提示你输入密码。





## 文件解压

### .zip 文件

如果遇到无法识别为 .zip 文件，可能是 zip 文件传输过程中损坏了，不完整，需要重新下或者重新传。

```bash
unzip archive.zip
```

#### 解压到指定目录

你可以使用 `-d` 选项指定目标目录：

```sh
unzip archive.zip -d /path/to/destination
```

- `-d /path/to/destination`：将文件解压到 `/path/to/destination` 目录。



### .tar.part 文件

如果你的压缩文件被分成了多个部分，通常是以.part1、.part2、part3 等形式命名的，那么你需要先将它们合并成一个完整的压缩文件，然后再进行解压缩。

假设你的压缩文件被分成了三个部分，分别是 file.tar.gz.part1、file.tar.gz.part2、file.tar.gz.part3, 可以使用以下命令将它们合并成一个完整的压缩文件：

```sh
cat file.tar.gz.part* > file.tar.gz
```

这条命令中，`*` 表示匹配所有以 `.part` 开头的文件，`>` 表示将输出重定向到一个新文件中。
接着，可以使用以下命令解压缩文件：

```sh
tar -zxvf file.tar.gz
```



### tar.gz 或.tgz 文件

语法格式如下：
```sh
tar -xzvf 文件名.tar.gz
```

- X 表示解压

- Z 表示使用 gzip 解压

- V 表示显示详细过程

- f 表示文件名

- -C 解压到特定文件夹

例如：

```sh
tar -xzvf example.tar.gz
```


这样就可以将 example..tar.gz 文件解压到当前目录。



**解压文件到指定目录**：

如果文件是 `.tar` 格式，你可以使用以下命令：

```bash
tar -xvf filename.tar -C /path/to/destination/directory/
```



如果文件是 `.tar.gz` 或 `.tgz` 格式，你应该使用：

```bash
tar -zxvf filename.tar.gz -C /path/to/destination/directory/
```



## 同时解压多个 tgz 文件

如果你想将所有解压的内容合并到一个新的目录中，可以先创建这个目录，然后将所有文件解压到这个目录里：

```sh
mkdir merged_files
for file in *.tgz; do tar -xzf "$file" -C /path/to/merged_files
```

tips: 慎用，文件太大容易崩





## 控制文件解压（是否覆盖原有文件）

当你使用 `tar -xzvf` 命令将一个 tar 归档文件解压到一个已经包含了相同文件名的特定目录时，`tar` 命令将会覆盖该目录中存在的同名文件，除非你使用了某些选项来避免这种情况。

如果你想避免覆盖已存在的文件，可以使用以下几种方式之一：

1. 使用 `--no-overwrite` 或 `-u` 选项来告诉 `tar` 只更新那些比存档中的副本更旧的文件。如果目标文件比存档中的新或者与之相同，`tar` 就不会提取这些文件。

   ```bash
   tar -xzvf archive.tar -C /path/to/directory --no-overwrite
   ```

2. 如果你想完全避免任何文件被覆盖，并且希望跳过所有已存在的文件，你可以使用 `--skip-old-files` 选项：

   ```bash
   tar -xzvf archive.tar -C /path/to/directory --skip-old-files
   ```

3. 如果你只想查看哪些文件会被提取而不实际执行解压操作，可以使用 `-t` 选项列出归档中的文件：

   ```bash
   tar -tzvf archive.tar
   ```

   这样你可以检查是否有重复的文件名，然后再决定是否进行解压。

4. 如果你想手动控制解压过程，可以在解压之前先检查目标目录的内容，并手动决定如何处理每个文件。

请注意，上述命令中的 `/path/to/directory` 应该替换为你想要解压到的实际目录路径，而 `archive.tar` 则是你要解压的归档文件名。

另外，如果你正在解压的是一个 `.tar.xz` 文件，命令会略有不同，因为 `.xz` 文件需要使用 `--xz` 或 `-J` 选项来指定解压算法：

```bash
tar -xJvf archive.tar.xz -C /path/to/directory
```

同样地，你可以结合使用上面提到的选项来控制文件覆盖行为



Tips：

如果你是在询问使用 `tar -xzvf` 命令解压文件时如果 **不加任何额外参数**（例如 `--no-overwrite`, `--skip-old-files`）时的行为，那么默认情况下，`tar` 命令会提取归档中的所有文件和目录，并且会覆盖目标目录中任何同名的现有文件，不会给出警告或提示。



## 找文件

```sh
find -name filename
```

1. **使用 `ls` 命令配合条件判断**
   虽然直接用 `ls` 命令判断文件存在与否不太推荐（因为它主要用于列出文件而非测试存在性），但你可以在某些上下文中结合使用它和命令的退出状态码。

```bash
ls /path/to/file > /dev/null 2>&1
if [ $? -eq 0 ]; then
    echo "文件存在"
else
    echo "文件不存在"
fi
```



1. **`ls /path/to/file > /dev/null 2>&1`**
   - `ls /path/to/file`: 尝试使用 `ls` 命令列出指定路径 `/path/to/file` 的文件信息。如果文件存在，`ls` 命令会正常执行并不显示任何输出，因为通常情况下 `ls` 命令用于列出目录内容，直接对单个文件使用时并不打印额外信息。
   - `> /dev/null`: 这部分将 `ls` 命令的标准输出（正常输出，文件信息）重定向到 `/dev/null`，这意味着即使有输出也会被丢弃，不会显示在终端上。
   - `2>&1`: 这是一个重定向操作符，它将标准错误（stderr，错误信息输出，编号为 2）重定向到与标准输出（stdout，编号为 1）相同的地方，在这个例子中就是 `/dev/null`。因此，任何因文件不存在而导致的错误消息也会被丢弃。
2. **`if [ $? -eq 0 ]; then`**
   - `$?`: 这个变量保存了 **上一个命令的退出状态码**。在 Unix/Linux 中，命令执行成功通常返回 0 作为退出状态码，而任何非零值通常表示有错误发生。
   - `-eq 0`: 这是条件测试表达式的一部分，用来检查上一个命令（在这里是 `ls` 命令）的退出状态码是否等于 0。
   - `[ ... ]`: 这是测试命令的语法，用于执行条件判断。当内部表达式为真时，它返回 0（成功），否则返回非零值。
   - 因此，`if [ $? -eq 0 ]; then` 这一段的意思是，如果上一个命令（`ls`）执行成功（即文件存在），则执行紧接着的 `then` 后面的命令。



### 查找指定类型，指定查找深度

找文件使用 `find` 命令通常更强大，因为它可以递归地查找子目录，并且可以过滤出你只想要的目录:

```bash
find . -type d
```

这里 `.` 代表当前目录，`-type d` 表示只查找类型为目录的条目。

如果你不希望在结果中包含当前目录(`.`)和父目录(`..`)，可以进一步修改 `find` 命令如下：

```bash
find . -mindepth 1 -maxdepth 1 -type d
```

这个命令中的 `-mindepth 1` 意味着至少深入一层目录结构，而 `-maxdepth 1` 意味着最多深入一层目录结构，因此它只会列出直接位于当前目录下的子目录。







## 黑洞文件

`/dev/null` 是 Linux 和类 UNIX 系统中的一个特殊文件，它代表一个“位桶”（bit bucket）或者称为黑洞。它的行为特性是任何写入到 `/dev/null` 的数据都会被丢弃，而尝试从 `/dev/null` 读取数据则会立即得到一个 EOF（End Of File）指示，表明没有数据可读。

`/dev/null` 的主要用途包括：

1. **丢弃输出**：当你不关心某个命令或程序的输出时，可以将输出重定向到 `/dev/null`，以此来避免这些输出干扰屏幕或日志文件。例如，`command > /dev/null` 会丢弃标准输出，而 `command 2> /dev/null` 会丢弃标准错误输出，`command &> /dev/null` 会同时丢弃标准输出和标准错误输出。
2. **抑制不需要的输出**：在编写脚本或运行命令时，有时为了减少不必要的信息显示，会将一些命令的输出导向 `/dev/null`，使程序更加干净地运行。
3. **作为占位符**：在需要指定一个文件但又不希望实际读写任何数据的情况下，可以使用 `/dev/null`。例如，某些命令要求提供一个输出文件名，但你不想保留输出时，就可以指定 `/dev/null`。
4. **测试和调试**：在进行系统或程序调试时，有时候会暂时将输出重定向到 `/dev/null` 来排除某些输出对问题分析的干扰，或者验证程序是否在没有输出依赖的情况下也能正常运行。

总之，`/dev/null` 是一个非常有用的工具，它帮助用户和系统管理员有效地管理输出流，提高脚本和命令行操作的效率与清晰度。





## 软连接

软连接的作用和创建

[Linux ln 命令 | 菜鸟教程 (runoob.com)](https://www.runoob.com/linux/linux-comm-ln.html)



软连接的删除

[Linux 怎么取消软链接_ln -s linux 怎么断开软链接-CSDN 博客](https://blog.csdn.net/dufufd/article/details/68943825)



## 文件权限

查看文件归属的用户：





权限不足会出现 Permission denied 的情况

[Linux 的文件访问权限及修改权限命令 chmod - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/44162944)









# Screen

关于守护进程：

[理解 Daemon 的真正含义 - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/32199628)



参考文章：

[终端命令神器--Screen 命令详解。助力 Unix/Linux 使用和管理 - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/405968623)



[远程神器 screen 命令的保姆级详解教程+举例-CSDN 博客](https://blog.csdn.net/weixin_39925939/article/details/121033427)



## 安装 screen

因为 screen 是“元老级”的 GNU 计划项目，所以不管是 **apt 软件源** *、或者是* **yum 软件源** 等其他软件源，都存在 screen，只需要使用软件源安装命令即可：

```bash
# CentOS
yum install screen
# Debian/Ubuntu
apt install screen
```

比如：***[腾讯云轻量应用服务器的 Debian 镜像](https://link.zhihu.com/?target=https%3A//curl.qcloud.com/IqpjH5MF)***，是纯净的 Debian 镜像，并没有自带 screen 的，输入 screen，会提示 `screen: command not found`，但是我们可以使用 `apt` 命令进行安装：

![img](https://pic2.zhimg.com/80/v2-64878d552af1605fb498fc505c9b5c21_1440w.webp)

之后，即可使用 screen 命令：

![img](https://pic3.zhimg.com/80/v2-b8d4c8c73bfa119c2ef83b2c13a7fc16_1440w.webp)

screen 安装成功



查看是否安装成功：

```bash
# 查看screen安装地址
which screen

# 查看screen版本
screen -v
```



## screen 命令集

screen，通常的命令格式为：

```scss
screen [-opts] [cmd [args]]
```

通常情况下，使用一下 `基础命令` 即可，`高阶命令` 过多，比较难记。

注意：

- 命令区分大小写

下文介绍针对 screen 命令集，对应的： - 状态介绍 - 基础命令 - 高级命令



## 状态介绍

通常情况下，screen 创建的虚拟终端，有两个工作模式：

![img](https://pic2.zhimg.com/80/v2-715dbf55f44fc5044e25e858a2bcec3d_1440w.webp)

screen 的两种状态模式

- ***Attached***：表示当前 screen 正在作为主终端使用，为活跃状态。
- ***Detached***：表示当前 screen 正在后台使用，为非激发状态。

通常情况下，不需要关注上面的状态。



## 常用指令

```bash
# 帮助文档
screen -help

# 查看已创建的虚拟终端
screen -ls

# Reattach现有虚拟终端，或创建一个名为yes的虚拟终端
screen -R yes

# detach其他位置名为name的虚拟终端
screen -d name
# reattach，将名为name的虚拟终端作为主终端使用（可以理解为进入对应虚拟终端）
screen -r name

# detach退出当前虚拟终端
ctrl+a d

# 删除虚拟终端
# 也可以在虚拟终端中输入exit
screen -R [pid/Name] -X quit

# 进入查看模式（可以用鼠标上下滚动）
ctrl a + Esc
```





# 主机间通信（传文件）

## Xftp（window 传 linux）

[Xftp 下载安装并远程 Ubuntu，实现文件传输【Xftp 走 ssh 协议而非 ftp 协议】_哔哩哔哩_bilibili](https://www.bilibili.com/video/BV1MD421V725/?spm_id_from = 333.337.search-card.all.click&vd_source = 3659941460e6c74679750d458eaa5726)

注意外网传学校内网服务器需要配置内网穿透，主机 ip 映射到内网穿透地址



## scp（linux 间互传，同一局域网）

示例命令：

```sh
scp -r -P 22 /home/data1/lurj22 lurj22@120.210.89.161:/home/data1/lurj22
```

-P 指定传输端口

-r 复制文件夹



主要方法：

在同一局域网内，两台 Linux 机器之间传输文件有多种方法，以下是其中一些常见的：

1. **使用 `scp` 命令** `scp`（secure copy）是一个基于 SSH 协议的安全文件复制工具，可以用于在两台机器间复制文件或目录。

   ```
   scp [options] <source> <destination>
   ```

   例如，从本地机器复制文件到远程机器：

   ```bash
   scp file.txt user@remotehost:/path/to/destination/ .
   ```

   或者从远程机器复制文件到本地：

   ```
   scp user@remotehost:/path/to/file.txt .
   ```

2. **使用 `rsync` 命令** `rsync` 是一个用于文件同步的工具，它比 `scp` 更高效，因为它只会传输文件差异部分，而不是整个文件。

   ```
   rsync [options] <source> <destination>
   ```

   例如，同步本地目录到远程目录：

   ```
   rsync -avz --progress ./localdir/ user@remotehost:/path/to/destination/
   ```



其他方法：

1. **使用 `sftp` 或 `ftp`** `sftp`（SSH 文件传输协议）和 `ftp`（文件传输协议）都可以用于文件传输。`sftp` 更安全，因为它通过 SSH 加密连接。

   ```
   sftp user@remotehost
   ```

   然后使用 `put` 和 `get` 命令来传输文件。

2. **使用共享文件系统如 NFS 或 SMB** 你也可以设置一个共享文件系统，比如 NFS（Network File System）或 SMB（Server Message Block），这样可以直接在两台机器之间访问文件，就像它们是在本地一样。

每种方法都有其优缺点，选择哪种方法取决于你的具体需求，如安全性、效率、易用性和网络环境。例如，对于安全性和效率要求较高的场景，推荐使用 `rsync` 或 `scp`；而对于简单快速的文件传输， `sftp` 可能就足够了。











# GPU 使用情况

gpustat

nvidia-smi



# 环境变量

## 追加 PATH（切换 CUDA）

**追加到 `PATH` 的末尾**：

```sh
export PATH=$PATH:/usr/local/my_program/bin
```

这样做会在现有 `PATH` 的末尾添加新的路径 `/usr/local/my_program/bin`。当你执行命令时，系统会先搜索 `PATH` 变量中原有的路径，然后才会搜索新添加的路径。

**追加到 `PATH` 的开头**：

```sh
export PATH=/usr/local/my_program/bin:$PATH
```

这样做会在现有 `PATH` 的开头添加新的路径 `/usr/local/my_program/bin`。当你执行命令时，系统会先搜索新添加的路径，然后才会搜索 `PATH` 变量中原有的路径。这种方式可以确保你优先使用 `/usr/local/my_program/bin` 目录中的可执行文件。



tips：在命令行输入只对当前 shell 生效，如果要一直生效，要追加到 bashrc 里面

```sh
echo 'export PATH=/usr/local/cuda/bin:$PATH' >> ~/.bashrc
source ~/.bashrc
```







## 删除 PATH

### 确定要删除的路径

首先，要删除 `PATH` 中的特定路径，你需要知道要删除的路径。假设你要删除的路径是 `/usr/local/my_program/bin`。

### 使用 `sed` 命令编辑 `PATH`

使用 `sed` 命令可以方便地编辑 `PATH` 环境变量。你可以使用 `sed` 将要删除的路径从 `PATH` 中移除，并将修改后的 `PATH` 重新导出。

下面是一个示例：

```sh
export PATH=$(echo $PATH | sed -e 's#:/usr/local/my_program/bin##g')
```

这个命令会将 `/usr/local/my_program/bin` 从 `PATH` 中移除。你可以根据需要调整要删除的路径。



在 `sed` 命令中，正则表达式通常使用斜杠 `/` 作为分隔符，但是在替换路径这样包含斜杠的情况下，使用斜杠作为分隔符可能会导致错误。为了避免这种问题，我们可以选择一个不在要替换的路径中出现的特殊字符作为替换操作的分隔符。

在这个例子中，选择了 `#` 作为分隔符。这样可以避免与路径中的斜杠冲突，使命令更加清晰。

命令的含义是：

- `-e` 选项表示后面跟着要执行的 `sed` 命令。
- `'s#:/usr/local/my_program/bin##g'` 是一个 `sed` 替换命令，其中 `s` 表示替换操作的开始，`#` 是我们选择的分隔符，`:/usr/local/my_program/bin` 是要被替换的内容，空字符串表示删除，`g` 表示全局替换，即删除所有匹配项。



### 验证更改

运行 `echo $PATH` 命令来验证 `PATH` 环境变量是否已经修改，确保要删除的路径已经不在其中。

### 注意事项

- 这种方法只会在当前 shell 会话中移除路径。如果你想永久删除路径，需要在你的 shell 配置文件中移除对该路径的设置，并重新加载 shell 配置文件，使更改生效。
- 修改 `PATH` 环境变量时要小心，确保不要删除了系统所需的重要路径，否则可能会导致系统功能受损。





## ~/.bashrc 更改 cuda 和 g++的模版

```bash
export PATH=/usr/bin/g++:$PATH
export PATH=/usr/bin:$PATH
# export LD_LIBRARY_PATH=/usr/local/cuda-11.1/lib64:$LD_LIBRARY_PATH
# export PATH=/usr/local/cuda-11.1/bin:$PATH
CUDAVER=cuda-11.1
export PATH=/usr/local/$CUDAVER/bin:$PATH
export LD_LIBRARY_PATH=/usr/local/$CUDAVER/lib:$LD_LIBRARY_PATH
export LD_LIBRARY_PATH=/usr/local/$CUDAVER/lib64:$LD_LIBRARY_PATH
export CUDA_PATH=/usr/local/$CUDAVER
export CUDA_ROOT=/usr/local/$CUDAVER
export CUDA_HOME=/usr/local/$CUDAVER
export CUDA_HOST_COMPILER=/usr/bin/gcc
```





## `.swp` 文件

在 Linux 系统中，`.swp` 文件是由 `vim` 文本编辑器创建的交换文件。当你使用 `vim` 编辑文件时，它会在相同目录下创建一个以 `.swp` 为扩展名的隐藏文件，作为编辑过程中的临时备份。这个文件包含了你正在编辑的文件的内容，以防在编辑过程中发生意外（如系统崩溃或断电）导致数据丢失。

如果你在编辑 `.bashrc` 文件时看到了 `.bashrc.swp` 文件，这意味着你之前使用 `vim` 编辑过 `.bashrc`，并且 `vim` 在你退出时没有正确删除这个交换文件。通常情况下，当你再次使用 `vim` 打开 `.bashrc` 时，它会检测到这个交换文件，并提示你恢复或删除它。

如果你确定不需要恢复之前的编辑状态，可以安全地删除这个 `.swp` 文件。你可以使用以下命令删除它：

```bash
rm /home/yys23/.bashrc.swp
```

请注意，删除 `.swp` 文件不会影响你的 `.bashrc` 文件本身，它只会删除 `vim` 的临时备份。如果你想要避免这种情况，可以在 `vim` 中设置 `autowrite` 选项，这样 `vim` 会在你编辑文件时自动保存更改，减少 `.swp` 文件的出现。你可以在 `vim` 中输入以下命令来设置 `autowrite`：

```vim
:set autowrite
```

然后，你可以保存并退出 `vim`：

```vim
:wq
```

这样，下次你编辑 `.bashrc` 时，`vim` 就不会创建 `.swp` 文件了。





# 查看历史

## 查看命令历史

在 Linux 系统中，查看历史命令信息主要有以下几种方式：

1. **使用 `history` 命令**：
   - 直接在终端输入 `history` 并回车，将会显示你曾经执行过的命令列表。每条命令前有一个编号，可以用来快速引用之前的命令。
2. **上下箭头键**：
   - 在命令行界面，不输入任何命令的情况下，按上箭头键可浏览之前执行过的命令，按向下箭头键则反向浏览。
3. **Ctrl+R 搜索命令**：
   - 按下 `Ctrl+R` 键启动反向搜索功能，然后输入命令的一部分，系统会找到最近一次包含此字符串的命令。继续按 `Ctrl+R` 会查找更早的匹配项。
4. **`.bash_history` 文件**：
   - 用户的历史命令默认被保存在各自家目录下的 `.bash_history` 文件中。你可以使用文本编辑器（如 `nano ~/.bash_history` 或 `vim ~/.bash_history`）来查看这个文件的内容。
5. **使用 `history` 命令的选项**：
   - 例如，`history -n` 可以显示最近的 n 条命令（但请注意，直接使用 `-n` 可能并非所有系统都支持此选项，通常用于限制输出数量的选项是 `-c` 清空历史，或通过 `history | head -n 10` 查看前 10 条）。
   - `history -h` 可以查看 `history` 命令的帮助信息。

这些方法可以帮助你有效地管理和回顾在 Linux 终端中执行过的命令历史。



## 查看命令行输出？

在 Linux 中，直接查看某个命令的历史输出是不可能的，因为命令行界面并不自动保存每个命令的输出结果到历史记录中。命令历史（通过 `history` 命令访问）仅记录了你输入的命令及其编号，并不包括这些命令执行后的输出信息。

但是，有几种间接的方法可以帮助你回顾或重新获得之前命令的输出：

1. **重定向输出**：在最初执行命令时，你可以通过重定向将输出保存到文件中。例如，`command > output.txt` 会将 `command` 的输出保存到 `output.txt` 文件中，之后你可以随时查看这个文件来重现输出。
2. **使用脚本**：如果你预计需要查看某段命令的输出，可以在执行前使用脚本来记录整个会话，包括输入的命令和相应的输出。
3. **Terminal Emulator 的复制粘贴功能**：大多数终端模拟器允许你选择和复制之前命令的输出文本，只要输出没有被新的输出覆盖或者你没有关闭终端窗口。
4. **Shell 会话记录工具**：有些工具如 `script` 命令可以记录整个 shell 会话，包括输入和输出，到一个文件中。运行 `script session.log` 开始记录，`exit` 退出记录后，`session.log` 文件中将包含这一期间的所有输入和输出。
5. **第三方工具或插件**：某些高级终端模拟器或插件（如 Tilix, Terminator 等）提供了会话管理功能，能够保存整个会话的状态，包括命令输出，以便后续查看。

综上所述，虽然直接查看历史输出不具备原生支持，但通过上述技巧可以在一定程度上实现类似的需求。





## 清除 pip 下载缓存的命令

要清除 `pip` 的下载缓存，可以使用以下命令：

```
pip cache purge
```

这条命令会清除所有已下载的包缓存。如果你只想删除特定包的缓存，可以使用以下命令：

```sh
pip cache delete <package_name>
```

例如，如果你想删除 `Pillow` 的缓存，可以使用：

```sh
pip cache delete Pillow
```





# 组合操作

**管道 `|`**:

- 管道符号用于将前一个命令的输出作为后一个命令的输入。



# 判断两个文件夹中是否有文件重复

### 使用 `find` 和 `grep`

```bash
find /path/to/dir1 -type f | cut -d'/' -f3- > dir1_files.txt
find /path/to/dir2 -type f | cut -d'/' -f3- > dir2_files.txt
grep -Fx -f dir1_files.txt dir2_files.txt
```

这个方法首先分别列出两个目录中所有文件的相对路径（去掉前两层目录路径），然后使用 `grep` 命令找出两个文件中完全相同的行（即文件名）。

---



```
find /path/to/dir1 -type f | cut -d'/' -f3- > dir1_files.txt
```

这段命令分为三个主要部分执行一系列操作来提取目录 `dir1` 中所有文件的相对路径名（不包括前两级目录），并将结果保存到一个文本文件 `dir1_files.txt` 中。下面是详细解释：

1. **`find /path/to/dir1 -type f`**:
   - `find` 命令用于在指定目录树中查找文件。
   - `/path/to/dir1` 是你要搜索的目录路径。
   - `-type f` 参数告诉 `find` 命令只查找文件，不包括目录。
2. **管道 `|`**:
   - 管道符号用于将前一个命令的输出作为后一个命令的输入。在这里，`find` 命令的输出（即 `dir1` 目录下所有文件的绝对路径）被传递给了 `cut` 命令。
3. **`cut -d'/' -f3-`**:
   - `cut` 命令用于从每行文本中剪切出指定的列。
   - `-d'/'` 指定了字段的分隔符为正斜杠 `/`，意味着我们根据路径中的斜杠来分割字段。
   - `-f3-` 表示提取从第三个字段开始直到行尾的所有字段。在这个上下文中，前两个字段通常是 `./` 或 `../`，表示当前目录或上一级目录，所以我们从第三个字段开始提取，以去除这些前缀，只保留文件名及其相对于 `dir1` 的路径部分。
4. **`> dir1_files.txt`**:
   - 这是一个重定向操作符，它把前面命令的输出重定向到一个名为 `dir1_files.txt` 的文件中。这意味着所有经过 `cut` 处理后的文件路径（不包括前两级目录的相对路径）都会被保存到这个文件里。

综上所述，整个命令的作用是从 `/path/to/dir1` 目录下查找所有文件，并将这些文件的相对路径（从第三级目录开始的部分）保存到 `dir1_files.txt` 文件中。





发现输出到文件中的路径仍然是绝对路径，那可能是因为在处理路径时没有正确地去除绝对路径的部分。为了确保只保留文件名及其相对于特定目录的路径（去除前两级目录），我们可以稍微调整一下命令：

```bash
(cd /path/to/dir1 && find . -type f) | cut -d'/' -f2- > dir1_files.txt
```

这里做了一个小改动：

- 首先，使用 `(cd /path/to/dir1 && find . -type f)` 将当前目录暂时切换到 `/path/to/dir1` 再执行 `find` 命令。这样做之后，`find` 输出的路径会以 `.` 开头，即当前目录，相当于去除了最外层的 `/path/to` 部分。
- 接着，使用 `cut -d'/' -f2-` 命令，因为我们已经去掉了最外层目录，所以现在应该从第二级（也就是第一个实际的子目录名）开始提取，因此使用 `-f2-` 而不是 `-f3-`。

这样处理后，输出到 `dir1_files.txt` 的应该是相对于 `dir1` 目录的相对路径了。

---



```bash
grep -Fx -f dir1_files.txt dir2_files.txt
```

1. **`grep`**: 是一个强大的文本搜索工具，用于在输入数据中搜索匹配指定模式的行并输出。
2. **`-F`**: 这个选项告诉 `grep` 将待搜索的模式作为固定字符串（而不是正则表达式）对待。这意味着文件中的任何特殊字符都不会被解释为正则表达式的特殊元素。
3. **`-x`**: 这个选项要求匹配整个行，即只有当输入行完全匹配模式时才显示该行。换句话说，只有当一行完全相同时才会被视为匹配。
4. **`-f dir1_files.txt`**: 使用 `-f` 选项指定一个文件，该文件包含了待搜索的模式，即每一行都是一个模式。在这里，`dir1_files.txt` 是包含你想要在另一个文件中查找的模式（即文件名）的文件。
5. **`dir2_files.txt`**: 这是 `grep` 命令要搜索的文件，它包含了另一组文件名或路径。

综上所述，这个命令的作用是查找 `dir1_files.txt` 中的每一行（假设这些行是文件名或路径），并在 `dir2_files.txt` 中寻找完全相同的行。如果 `dir2_files.txt` 中有与 `dir1_files.txt` 中任何一个模式完全相同的行，`grep` 就会输出这些行，从而帮助你识别两个文件夹中具有相同文件名的文件。



# diff 指令

`diff` 是一个在类 Unix 系统中广泛使用的命令行工具，用于比较文件内容的差异。它可以帮助用户找出两个文件在哪些地方不同，常用于文本文件的版本控制、编程调试和文档修订等方面。以下是关于 `diff` 命令的一些基本用法和解释：

### 基本语法

```bash
diff [选项] 文件1 文件2
```

### 常用选项

- **`-q` 或 `--brief`**: 仅报告是否存在差异，不显示具体的差异内容。
- **`-c`**: 使用上下文输出格式，显示几行上下文以便更好地理解差异。
- **`-u` 或 `--unified`**: 使用统一上下文输出格式，这是程序员常用的格式，通常显示 3 行上下文。
- **`-w` 或 `--ignore-all-space`**: 忽略空白字符的不同。
- **`-B` 或 `--ignore-blank-lines`**: 忽略空白行的存在与否。
- **`-i` 或 `--ignore-case`**: 忽略大小写的区别。
- **`-l`**: 如果两个文件不相同，显示文件名并退出。

### 示例

1. **简单比较两个文件**:

```bash
diff file1.txt file2.txt
```

这将显示两个文件之间的所有差异。

1. **使用上下文输出格式**:

```bash
diff -c file1.txt file2.txt
```

显示差异时，每处差异前后各带几行上下文。

1. **忽略空白字符**:

```bash
diff -w file1.txt file2.txt
```

当你只关心内容差异，而不关心缩进或空格时，这个选项很有用。

1. **比较目录**:

```bash
diff -r dir1 dir2
```

这会递归比较两个目录中的所有文件。注意，这会比较文件名和内容，如果文件名不同，也会被标记为差异。

`diff` 命令的输出通常包括 `<`、`>` 或 `---`、`+++` 等标记来指示文件内容的增删改，以及使用 `@` 符号标记差异所在的行范围。掌握 `diff` 命令对于日常的文件管理和版本控制非常有帮助。



## 输出

1. < 和 >

在 `diff` 命令的输出中，尖括号 `<` 和 `>` 用于表示文件内容的变动情况：

- `<` 符号前的行表示这些行存在于第一个文件中（即“原文件”或“旧文件”），但在第二个文件中被删除或修改了。
- `>` 符号前的行表示这些行是新增加的，它们不存在于第一个文件中，而是出现在第二个文件中（即“新文件”）。



2. +++和---

```diff
--- file1.txt
+++ file2.txt
@@ -1,3 +1,3 @@
 This is an example
-Old line that has been removed.
+New line added instead.
 Another line remains the same.
```

这段输出说明：

- `file1.txt` 和 `file2.txt` 正在被比较。
- 第二行（在 `file1.txt` 中）被移除（以 `-` 开头）。
- 第二行（在 `file2.txt` 中）被新增（以 `+` 开头）。
- 第三行在两个文件中都存在，作为上下文显示。





# 查看当前机器上所运行的进程



`lsof` 是一个在类 Unix 操作系统上常用的命令行工具，用于列出当前打开的文件和网络连接。它的全称是 "list open files"。`lsof` 可以显示进程所打开的文件、设备、网络连接等信息，对于调试程序、查找资源占用情况非常有帮助。

在使用 `lsof` 时，你可以通过以下一些常见的选项来获取特定的信息：

- `-a`: 执行多个过滤条件。
- `-i`: 显示使用网络的进程。
- `-P`: 显示端口号。
- `-n`: 不解析主机名和端口名称。
- `-p <pid>`: 仅显示指定进程的信息。
- `-c <command>`: 显示由指定命令启动的进程信息。
- `-u <user>`: 显示指定用户的所有进程信息。

例如，如果你想要查看所有与网络相关的打开文件，可以使用：

```bash
lsof -i
```

查看占用特定端口的进程

```bash
lsof -i :<port>
```

这个命令会显示所有与该端口相关的网络连接和对应的进程信息。输出通常包括进程的 PID（进程 ID）、进程名称、以及端口的状态（如 LISTEN 表示监听状态）。



如果你想进一步确认是处于监听状态的连接，可以在命令后添加 `| grep "(LISTEN)"` 来过滤输出，如下所示：

```
lsof -i :8089 | grep "(LISTEN)"
```

这将只显示那些处于监听状态的连接，帮助你更准确地找到占用端口的进程。



注意：`lsof` 需要足够的权限才能运行，可能需要以 root 用户身份执行，或者使用 `sudo` 命令。



# 查看进程信息 ps

1. **确定进程 PID**： 在 `htop` 中，你可以看到 `./log` 进程的 PID（进程 ID）。记下这个 ID，以便后续操作。
2. **检查进程详情**： 使用 `ps` 或 `top` 命令加上 PID 来获取更多关于 `./log` 进程的信息。例如：

```bash
ps aux | grep <PID>
```

这可以帮助你了解进程的完整路径、所属用户、使用的资源等。

1. **分析日志或程序行为**： 如果 `./log` 是在记录日志，检查其产生的日志文件，看看是否有异常信息或循环执行的模式。这可能帮助你理解为什么它消耗如此多的 CPU 资源。
2. **优化程序**： 如果 `./log` 是你自己编写的程序，检查代码逻辑，寻找可能的优化点，比如不必要的循环、重复计算或低效的数据处理。考虑使用更高效的数据结构或算法。
3. **限制资源使用**： 你可以使用 `cpulimit` 工具来限制进程的 CPU 使用率。例如，要将 `./log` 的 CPU 使用限制在 50%，可以这样做：

```bash
cpulimit -l 50 -p <PID>
```

但是，这可能会影响程序的正常运行，所以要谨慎使用。



查看 python 相关进程

```bash
ps aux | grep python
```





## 杀进程

杀死所有有关 python 的进程

```bash
killall python
```





## 生成公钥和秘钥

`ssh-keygen` 是一个用于生成 SSH 密钥对的命令行工具。SSH 密钥对用于进行安全地登录远程服务器或执行操作，无需每次输入密码。以下是使用 `ssh-keygen` 的一些基本步骤和选项：

1. **生成密钥对**:

   ```
   ssh-keygen
   ```

   运行此命令后，系统会提示你输入几个信息：

   - 存储位置（默认为 `~/.ssh/id_rsa`）。
   - 密码短语（可选，用于保护私钥）。

2. **指定密钥类型**: 如果你想指定密钥类型（如 RSA 或 ED25519），可以这样做：

   ```
   ssh-keygen -t rsa
   ```

3. **指定文件名**: 你可以自定义密钥对的文件名：

   ```
   ssh-keygen -t rsa -f ~/.ssh/mykey
   ```

4. **无交互模式生成密钥**: 如果你想在脚本中自动创建密钥对，可以使用 `-N` 选项来避免交互式提示：

   ```
   ssh-keygen -t rsa -b 2048 -N '' -f ~/.ssh/mykey
   ```

   这里 `-N ''` 表示不设置密码短语。

5. **检查已有的密钥**: 你可以查看已生成的公钥文件（通常以 `.pub` 结尾），例如：

   ```
   cat ~/.ssh/id_rsa.pub
   ```

6. **添加密钥到 SSH 代理**: 为了方便使用，你可以将私钥添加到 SSH 代理中：

   ```
   ssh-add ~/.ssh/mykey
   ```

这些步骤可以帮助你生成并管理 SSH 密钥对，以便于安全地访问远程服务器。



[完美解决 WARNING: REMOTE HOST IDENTIFICATION HAS CHANGED!-阿里云开发者社区 (aliyun.com)](https://developer.aliyun.com/article/1397189)



## 向远程服务器配置公钥

将本地的 id_rsa.pub 公钥放到服务器上的 authorized_keys(/root/.ssh/authorized_keys).

   **（可以手动复制过去，也可以\**ssh-copy-id root@10.10.10.10\**）**





# Win 远程挂载 Linux 文件系统

https://www.cnblogs.com/linuxprobe/p/13747709.html

[Windows 下使用 SSHFS 通过 SSH 协议挂载远程服务器目录-CSDN 博客](https://blog.csdn.net/xieqiaokang/article/details/109557482)——原文链接：[Windows 下使用 SSHFS 通过 SSH 协议挂载远程服务器目录 | 谢乔康 | Qiaokang Xie (xieqiaokang.com)](https://blog.xieqiaokang.com/posts/505416489.html)



## linux 从网络上下载文件

### 解释指令 `wget -c -O v1.0-trainval01_blobs.tar "链接"`

这条指令的作用是从指定的 URL 下载文件，并保存为本地文件。

#### 具体解释：

- `wget`: 命令行工具，用于从网络下载文件。
- `-c`: 继续下载之前未完成的部分（断点续传）。
- `-O v1.0-trainval01_blobs.tar`: 将下载的文件保存为 `v1.0-trainval01_blobs.tar`。
- `"链接"`: 下载的 URL 地址。

### 更多 `wget` 参数和用法

#### 常用参数：

1. `-b`: 后台下载。
2. `-c`: 断点续传。
3. `-O <file>`: 指定输出文件名。
4. `-N`: 只在远程文件比本地文件新时才下载。
5. `-P <directory>`: 将下载的文件保存到指定目录。
6. `-q`: 安静模式，不显示进度信息。
7. `-t <number>`: 设置最大重试次数。
8. `-T <seconds>`: 设置超时时间（单位：秒）。
9. `-nv`: 不显示详细信息。
10. `-nd`: 不创建目录结构。
11. `-np`: 不爬取父目录。
12. `-r`: 递归下载整个目录。
13. `-A <file-pattern>`: 只下载匹配指定模式的文件。
14. `-H`: 递归下载时保留主机名。
15. `-U <user-agent>`: 设置 User-Agent 字符串。

### 示例用法：

1. **基本下载**：

   ```sh
   wget https://example.com/file.tar.gz
   ```

2. **断点续传**：

   ```sh
   wget -c https://example.com/file.tar.gz
   ```

3. **指定输出文件**：

   ```sh
   wget -O output.tar.gz https://example.com/file.tar.gz
   ```

4. **后台下载**：

   ```sh
   wget -b https://example.com/file.tar.gz
   ```

5. **只在文件更新时下载**：

   ```sh
   wget -N https://example.com/file.tar.gz
   ```

6. **递归下载整个目录**：

   ```sh
   wget -r https://example.com/directory/
   ```

7. **限制下载速度**：

   ```sh
   wget --limit-rate=100k https://example.com/file.tar.gz
   ```

通过这些参数和用法，你可以更灵活地使用 `wget` 进行网络文件下载。



# 其他命令

- `top`：显示系统资源使用情况。

  - `top`：显示实时的系统资源使用情况。

- `ps`：显示进程状态。

  - `ps aux`：显示所有用户的进程列表。

- `kill`：发送信号给进程。

  - `kill PID`：终止进程。

- `man`：显示命令的手册页。

  - `man command`：显示命令的使用手册。

  在 Linux 中，`man` 是 "manual"（手册）的缩写。它是一个命令行工具，用于查看系统中大多数命令、函数和配置文件的详细说明文档。当你在终端中输入 `man [命令名]` 时，比如 `man ls`，它会显示关于 `ls` 命令的手册页，提供详细的使用说明、选项列表以及其他相关信息。

  `man` 命令通常使用分页器（如 `less` 或 `more`）来显示文档内容，并且可以通过键盘上的箭头键、Page Up/Down 键或空格键进行滚动浏览。要退出手册页，通常可以按 `q` 键。

  

- `cat`：显示文本文件内容。
  
  - `cat filename`：显示文件内容。
- `grep`：搜索文件内容。
  
  - `grep pattern filename`：搜索文件中包含模式的行。



# 命令缩写

`df` 是 "disk free" 的缩写，用于显示文件系统的磁盘空间使用情况。



`wc` 是 "word count" 的缩写，是一个用于统计文件中字数、行数和字符数的命令。`wc` 命令在终端中使用，可以帮助用户快速获取文件内容的统计信息。



`cat` 是 "concatenate" 的缩写，是一个用于显示文件内容、连接文件、创建文件的命令。`cat` 命令在终端中使用广泛，常用于查看文本文件内容、合并文件内容、以及创建新文件。



`ln` 是 "link" 的缩写，用于创建链接文件，即创建一个文件的链接或快捷方式。`ln` 命令可以创建硬链接或符号链接（软链接），用于在文件系统中创建文件之间的关联。



`touch` 命令的原意是触摸，它最初的作用是“触摸”文件，即更改文件的访问和修改时间戳，而不是修改文件的实际内容。这样做可以帮助管理文件的时间属性，例如创建一个空文件或者更新文件的时间戳，而不必实际修改文件内容。



`du` 命令是 "disk usage"（磁盘使用情况）的缩写。这个命令用于估算文件或目录所占用的磁盘空间。通过 `du` 命令，可以查看单个文件、多个文件以及整个目录的磁盘使用情况。常用的选项和用途如下：



`chmod` 的原本英文单词是 "change mode"，翻译成中文是 "改变模式"





# 安装 miniconda

在 Linux 上安装 Miniconda，你可以按照以下步骤操作：

1. **打开终端**：首先，打开你的 Linux 系统的终端。
2. **下载安装脚本**：使用 `wget` 或 `curl` 命令下载 Miniconda 的安装脚本。这里以获取最新版本的 Miniconda 3 为例：

```
wget https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh
```

[Download Now | Anaconda](https://www.anaconda.com/download/success)

或者，如果你需要特定版本，如 Python 3.7，可以替换 URL 中的 `latest` 为相应的版本号，例如：

```
wget https://repo.anaconda.com/miniconda/Miniconda3-py37_4.12.0-Linux-x86_64.sh
```

1. **赋予执行权限**：下载完成后，需要给安装脚本赋予执行权限：

```
chmod +x Miniconda3-latest-Linux-x86_64.sh
```

1. **运行安装脚本**：接下来，运行安装脚本。在运行之前，你可以通过添加 `-b` 参数来进行静默安装，并通过 `-p` 参数指定安装路径，例如安装到 `~/miniconda3`：

```
./Miniconda3-latest-Linux-x86_64.sh -b -p ~/miniconda3
```

如果不使用静默安装，脚本会引导你完成安装过程，期间可能需要你阅读并接受许可协议。

1. **验证安装**：安装完成后，关闭并重新打开终端，然后运行以下命令来验证 Conda 是否安装成功：

```
conda --version
```

1. **（可选）初始化环境**：首次使用 Miniconda，你可能需要初始化 conda 环境：

```
source ~/miniconda3/bin/activate
```

这样就完成了 Miniconda 在 Linux 上的安装。记得根据实际情况调整命令中的路径和版本信息。



## 删除除了base之外的所有环境（清理环境）

- 要删除 Conda 除了 `base` 之外的所有环境，可以按照以下步骤操作：

1. **列出所有环境**：

   ```
   conda env list
   ```

2. **删除所有非 `base` 环境**：

   ```
   conda env list | grep -v "base" | awk '{print $1}' | xargs -I {} conda env remove --name {}
   ```

   这条命令的解释：

   - `conda env list`：列出所有 Conda 环境。
   - `grep -v "base"`：过滤掉 `base` 环境。
   - `awk '{print $1}'`：提取环境名称。
   - `xargs -I {} conda env remove --name {}`：对每个环境名称执行 `conda env remove --name` 命令。

3. **验证所有非 `base` 环境是否已删除**：

   ```
   conda env list
   ```

   确认输出中只有 `base` 环境。

这样可以确保除了 `base` 环境之外的所有环境都被删除



# conda 环境迁移：

 [【conda】实现 conda 环境迁移的 4 种方式_conda 环境移植-CSDN 博客](https://blog.csdn.net/baidu_35692628/article/details/136519579) 

有时候里面的包有使用 pip install -e 安装的，需要使用参数--ignore-editable-packages，可以使用 conda-pack --help 查看



不能直接复制 env 文件夹





方案 1: 使用 conda pack 制作压缩包并在目标环境解压使用
适合离线环境, 在目标环境无法联网或者网络不畅时很好用

**(1) 先安装 conda pack**

pip install conda-pack

或者

conda install conda-pack

**(2) 查看要打包的 conda 环境**

conda info -e

**(3) 压缩 conda 环境**

conda pack -n your_conda_env	# 会自动压缩为 your_conda_name.tar.gz
或

conda pack -n your_conda_env -o out_name.tar.gz	# 自定义压缩包名

或

conda pack -p /your/path/to/your_conda_env	# 打包指定目录下的环境


**(4) 将压缩包拷贝到目标环境**
目标环境需要和源环境是相同平台和操作系统



**(5) 在目标环境 anaconda/env 下创建文件夹并解压**

cd ~/anaconda/env
mkdir your_conda_name
cd your_conda_name
sudo tar -zxvf your_conda_env.tar.gz

**(6) 查看并使用 conda 环境**

conda info -e
conda activate your_conda_env



## conda-pack 常见问题

1、使用可编辑模式安装的包

![6e645f4eb2328ad6ea12a7ed01a2dd9](../../Documents/WeChat Files/wxid_jtn4w46azqfg22/FileStorage/Temp/6e645f4eb2328ad6ea12a7ed01a2dd9.png)

2、conda 和 pip 版本不匹配导致冲突

解决方案：添加 `--ignore-missing-files` 参数

如：`conda pack -p /home/yys23/envs/vidar -o vidar_env.tar.gz --ignore-editable-packages --ignore-missing-files`



参考：

[CondaPackError ： 发现由 conda 管理的文件已被删除/覆盖 ·问题 #98 ·conda/conda-pack --- CondaPackError : Files managed by conda were found to have been deleted/overwritten · Issue #98 · conda/conda-pack (github.com)](https://github.com/conda/conda-pack/issues/98)

另外的解决方法：（未尝试）

[【Pytorch】Conda 环境 pack 打包迁移报错处理_`pip install -e`). editable packages found:-CSDN 博客](https://blog.csdn.net/qq_36693514/article/details/140362776)



# 注意：

要注意所使用pip的位置，which pip  可以看，不要用到全局的pip了，这样的话会把包安装在全局，而不是虚拟环境里。

- 使用 `conda` 创建环境时，默认情况下不会自动安装 `pip`。如果你希望创建一个不包含 `pip` 的环境，可以使用以下命令：

```bash
conda create --name myenv
```



- 如果你之后需要在该环境中安装 `pip`，可以使用以下命令：

```
conda install pip
```



- **如果在创建环境的时候需要pip，可以直接指定python版本**

```bash
conda create --name myenv python==3.7
```

tips：因为配置环境花费了很多时间，以后遇到这种疑似机器出错的问题，请保持理性，分析一下，一步一步求证。



# .condarc

要使`.condarc`文件生效，你需要确保以下几点：

1. **文件位置正确**：`.condarc`文件应该位于你的用户主目录下，即`~/.condarc`。如果文件不在这个位置，你需要将其移动到正确的位置。
2. **文件内容正确**：确保`.condarc`文件中的内容是正确的，并且没有语法错误。以下是一个示例`.condarc`文件的内容：

```plaintext
channels:
  - defaults
show_channel_urls: true
default_channels:
  - https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/main
  - https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/r
  - https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/msys2
custom_channels:
  conda-forge: https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud
  msys2: https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud
  bioconda: https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud
  menpo: https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud
  pytorch: https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud
  simpleitk: https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud
```

1. **刷新配置**：在修改`.condarc`文件后，你需要刷新conda的配置，以便它能够读取新的配置信息。你可以使用以下命令来刷新配置：（去掉system就是只刷新当前用户，system是全局）

```bash
conda config --system --set show_channel_urls yes
```

1. **验证配置**：你可以使用以下命令来验证`.condarc`文件是否已经生效：

```bash
conda config --show
```

这个命令会显示当前的conda配置，包括`.condarc`文件中的设置。

1. **重启终端**：有时候，即使你已经刷新了配置，新的设置可能不会立即生效。在这种情况下，你可以尝试重启终端，然后再次检查配置是否已经生效。



# 设置pip的源

你可以在命令行中使用以下命令：

```bash
pip config set global.index-url https://pypi.tuna.tsinghua.edu.cn/simple
```

这个命令会修改你的pip配置文件，将默认的源设置为清华源。如果你想要验证是否已经成功设置，可以使用以下命令来查看当前的配置：

```bash
pip config list
```

这将显示你的pip配置，包括默认的源。如果你看到`index-url`的值是`https://pypi.tuna.tsinghua.edu.cn/simple`，那么说明已经成功设置了清华源。



# 配置多个源

1. 输入以下命令来编辑pip配置文件：

   ```bash
   pip config edit
   ```

2. 在打开的配置文件中，添加以下内容：

   ```ini
   [global]
   index-url = https://pypi.tuna.tsinghua.edu.cn/simple
   extra-index-url = https://pypi.python.org/simple
   ```

   这将设置清华源为默认源，并将Python官方源作为备用源。

3. 保存并关闭配置文件。

现在，当你使用pip安装包时，它会首先尝试从清华源下载，如果清华源中没有该包，它会自动尝试从Python官方源下载。

```
# 清华源
pip config set global.index-url https://pypi.tuna.tsinghua.edu.cn/simple
# 阿里源
pip config set global.index-url https://mirrors.aliyun.com/pypi/simple/
# 腾讯源
pip config set global.index-url http://mirrors.cloud.tencent.com/pypi/simple
# 豆瓣源
pip config set global.index-url http://pypi.douban.com/simple/# 换回默认源pip config unset global.index-url
```

```
# 换回默认源
pip config unset global.index-url
```

[Python 修改 pip 源为国内源 - 点点米饭 - 博客园 (cnblogs.com)](https://www.cnblogs.com/137point5/p/15000954.html)







# 重命名 conda 环境

从[Conda 4.14](https://github.com/conda/conda/milestone/55)版本开始，你可以使用以下命令来改变环境名称：

```lua
conda rename -n old_name new_name
```

虽然在内部，`conda rename`仍然使用了[[1\]](https://github.com/conda/conda/pull/11496/files#diff-2cf7ba1d1799c57376f2066177b166979c8f6854a2540c4dd5077f0b95031b93R241)[[2\]](https://github.com/conda/conda/pull/11496/files#diff-66bae0eac87592b832fa7e85ad41263739a925b211d4b2f386385092e7df3ca4)中提到的`conda create`和`conda remove`的组合方式。

使用`-d`选项进行干运行（v22.11.0及更高版本不是目标目录）

```lua
conda rename -n old_name -d new_name
```

## 







# 用户管理

`/etc/passwd` 文件包含了系统中所有用户的详细信息。你可以使用 `cat` 命令来查看整个文件，或者使用 `grep` 命令来过滤特定用户。

#### 查看所有用户信息

```
cat /etc/passwd
```

如果你是root用户，想要**修改其他用户的密码**，可以使用以下命令：

```sh
passwd username
```

如果你是管理员，想要修改用户的主目录，可以使用 `usermod` 命令。例如，要将用户 `username` 的主目录更改为 `/new/home/directory`，可以使用以下命令：

```sh
usermod -d /new/home/directory username
```

请注意，这个命令只会更改用户的主目录路径，不会移动用户的文件。如果你想要将用户的文件也移动到新的主目录，你需要使用 `-m` 选项：

```sh
usermod -d /new/home/directory -m username
```

这个命令会将用户的主目录路径更改为 `/new/home/directory`，并且将用户的文件从旧的主目录移动到新的主目录。



#### 添加用户

```sh
sudo adduser zls
```

#### 授予用户 sudo 权限

##### 1. 将用户添加到 sudo 组

在大多数 Linux 发行版中，`sudo` 组的成员拥有 sudo 权限，可以通过以下命令将新用户添加到 sudo 组：

```bash
sudo usermod -aG sudo new_user
```

这里的 `-aG` 参数组合表示追加（append）用户到指定组（group），不移除其原有的其他组成员资格。



##### 2. 直接编辑 sudoers 文件（不推荐，有风险）

如果你需要更细致的 sudo 权限控制，可以直接编辑 `/etc/sudoers` 文件，但这通常通过 `visudo` 命令完成，而不是直接使用 `vim` 或其他文本编辑器，因为 `visudo` 可以确保文件在编辑过程中保持正确格式且防止意外锁定：

```bash
sudo visudo
```

然后在编辑器中，在适当的位置（比如“用户规范”区域）添加类似以下行的内容：

```bash
new_user ALL=(ALL) ALL
```

这条规则意味着新用户 `new_user` 可以以任何用户身份在任何主机上执行任何命令。保存并退出编辑器。

##### 3. 注意事项：

- 修改 `/etc/sudoers` 文件时务必小心，错误的配置可能会导致无法使用 sudo 命令甚至锁死系统。
- 在现代 Linux 系统中，将用户添加到 sudo 组通常是给予管理员权限的标准做法。
- 若想撤销 sudo 权限，可以从 sudo 组中移除用户，但不能直接从 `/etc/sudoers` 文件中删除对应行，除非你确切知道正在做什么。

##### 4. 其他用户管理操作：

- 删除用户（包括其家目录）：

  ```bash
  sudo userdel -r new_user
  ```

- 修改用户账户属性（如用户 ID、组 ID 等）：

  ```bash
  sudo usermod -u 新UID new_user
  sudo usermod -g 新GID new_user
  ```

- 查看用户信息：

  ```bash
  id new_user
  ```

- 切换用户：

  ```bash
  su - new_user
  ```

或者使用 `sudo` 登录为其他用户（如果当前用户有 sudo 权限）：

```bash
sudo su - new_user
```

### **移除用户的 sudo 权限**

有时，你可能希望移除特定用户的 `sudo` 权限，而不用在 Linux 中删除它。要将任何用户设为普通用户，只需将其从 `sudo` 组中删除即可。

比如说如果要从 `sudo` 组中删除名为 `ostechnix` 的用户，只需运行：

```text
$ sudo deluser ostechnix sudo
```

示例输出：

```text
Removing user `ostechnix' from group `sudo' ...
Done.
```

此命令仅从 `sudo` 组中删除用户 `ostechnix`，但不会永久地从系统中删除用户。现在，它成为了普通用户，无法像 `sudo` 用户那样执行任何管理任务。

此外，你可以使用以下命令撤消用户的 `sudo` 访问权限：

```text
$ sudo gpasswd -d ostechnix sudo
```

从 `sudo` 组中删除用户时 [请小心](https://zhida.zhihu.com/search?content_id=100992651&content_type=Article&match_order=1&q=请小心&zhida_source=entity)。不要从 `sudo` 组中删除真正的管理员。

使用命令验证用户 `ostechnix` 是否已从 `sudo` 组中删除：

```text
$ sudo -l -U ostechnix
User ostechnix is not allowed to run sudo on ubuntuserver.
```

是的，用户 `ostechnix` 已从 `sudo` 组中删除，他无法执行任何管理任务。

从 `sudo` 组中删除用户时请小心。如果你的系统上只有一个 `sudo` 用户，并且你将他从 `sudo` 组中删除了，那么就无法执行任何管理操作，例如在系统上安装、删除和更新程序。所以，请小心。

撤错了也别紧张，只要你会话没断，用户组在当前会话还会是没改之前的，换句话说更改用户组只有重新登录才能生效，再加回来就是了





# 设置所有者和权限

在Linux中，你可以使用`chmod`命令来更改文件夹的权限，使其对所有用户都可访问。以下是一个详细的步骤说明：

1. 首先，使用`cd`命令进入到你想要设置权限的文件夹所在的目录。例如：

   ```sh
   cd /path/to/your/folder
   ```

2. 然后，使用`chmod`命令来更改文件夹的权限。`chmod`命令的基本语法是：

   ```sh
   chmod [选项] 权限模式 文件名
   ```

   权限模式可以使用数字表示，也可以使用符号表示。对于所有用户都可访问的权限，你可以使用数字模式`777`，或者符号模式`a+rwx`。

   - 数字模式`777`表示：
     - 第一个`7`：文件所有者（user）具有读（4）、写（2）、执行（1）权限。
     - 第二个`7`：文件所属组（group）具有读（4）、写（2）、执行（1）权限。
     - 第三个`7`：其他用户（others）具有读（4）、写（2）、执行（1）权限。
   - 符号模式`a+rwx`表示：
     - `a`：所有用户（all）。
     - `+`：添加权限。
     - `rwx`：读（read）、写（write）、执行（execute）权限。

3. 例如，使用数字模式`777`来设置权限，命令如下：

   ```sh
   chmod 777 /path/to/your/folder
   ```

   或者使用符号模式`a+rwx`来设置权限，命令如下：

   ```sh
   chmod a+rwx /path/to/your/folder
   ```

4. 执行上述命令后，文件夹的权限就会被设置为所有用户都可访问。



### 设置所有者：

chown -R zhuls24:zhuls24 /folder

-R表示递归处理文件夹下的所有文件，将下面的所有文件都设置为zhuls24拥有





## 切换 g++

下载多个g++和gcc**（注意g++和gcc版本需要对应！！！！）**

```sh
sudo apt install gcc-9 	# -y 它的作用是在安装过程中自动回答“是”（yes）以确认所有的提示和警告。
```

下载路径一般会在/usr/bin中，只需要修改软连接/usr/bin的指向就可以了



如果 g++的路径为/usr/bin/g++，则需要在环境变量前面追加/usr/bin/而不是/usr/bin/g++

查看目前使用的 g++路径

```sh
which g++
```



查看目前使用的 g++版本

```sh
g++ --version
```



查看目前机器上有的 g++

```sh
whereis g++
```



查看 whereis g++ 输出的路径中，每一个路径所对应的版本，如/usr/bin/g++

```sh
/usr/bin/g++ --version
```



查看路径是否是一个符号链接

```sh
ls -l /usr/bin/g++
```

若果输出如 `lrwxrwxrwx 1 root root 31 5月  26 16:09 /usr/bin/g++ -> /usr/bin/x86_64-linux-gnu-g++-7`

则表示/usr/bin/g++ 是一个指向/usr/bin/x86_64-linux-gnu-g++-7 的符号链接。



然后你可以

**删除旧的符号链接**：

```sh
sudo rm /usr/bin/g++
```

**创建新的符号链接**：

```sh
sudo ln -s /usr/bin/g++-11 /usr/bin/g++
```

-s表示soft，软连接



# 安装cuda和cudnn

[CUDA与cuDNN在linux / Ubuntu22.04上的安装与卸载，包含CUDA的.run安装与.deb安装，cuDNN的.tar安装与.deb安装_cudnn卸载-CSDN博客](https://blog.csdn.net/weixin_47937828/article/details/141233249)

使用conda管理环境的话，一般会自带cudnn，可以不用在意版本。

服务器上安装了cudnn-cuda-11，如果要用cudnn-cuda-12，需要sudo apt-get install -y重新安装一下

编译时请将官方测试脚本移到可以写的目录，如$HOME[【最新】cuDNN在CUDA11.7+Ubuntu20.04下的安装及卸载_cuda11.7对应的cudnn-CSDN博客](https://blog.csdn.net/weixin_54470372/article/details/127473509)

 



[Ubuntu20.04下CUDA、cuDNN的详细安装与配置过程（图文）_ubuntu cudnn安装-CSDN博客](https://blog.csdn.net/weixin_37926734/article/details/123033286)

官网链接：

[CUDA Toolkit 11.7 Update 1 Downloads | NVIDIA Developer](https://developer.nvidia.com/cuda-11-7-1-download-archive?target_os=Linux&target_arch=x86_64&Distribution=Ubuntu&target_version=22.04&target_type=runfile_local)



[cuDNN 9.5.0 Downloads | NVIDIA Developer](https://developer.nvidia.com/cudnn-downloads?target_os=Linux&target_arch=x86_64&Distribution=Ubuntu&target_version=22.04&target_type=deb_local)

其他版本的cudnn：[cuDNN Archive | NVIDIA Developer](https://developer.nvidia.com/cudnn-archive)









# linux、windows 配置梯子calsh

[最全 Linux 科学上网三种方式，ubuntu 使用 clash 客户端，带桌面，不带桌面，docker 容器，终端代理，clash ui 设置快捷方式与系统命令 一键启动客户端 (youtube.com)](https://www.youtube.com/watch?v=VOlWdNZAq_o)

前期准备：机场提供的配置文件

linux 中主要使用了 clash-core，[Releases · Kuingsmile/clash-core (github.com)](https://github.com/Kuingsmile/clash-core/releases)

![image-20241011203652011](https://raw.githubusercontent.com/ZZZRamsey/PicGo_save/main/202410112037219.png)

tips：视频教程中还教了如何把 clash 封装成系统服务，如何导入外部 ui 界面（可以在局域网中其他机器访问界面），并且还提到了如何使用 docker 启动



测试

```sh
curl -i google.com
```





# ssh 连接问题

![AgA2fc4neb](D:/ShareX_save/2024-10/AgA2fc4neb.png)

解决方法：

把本地电脑的 known_host 和服务器电脑的 known_host 中的关于对方的信息全删掉，比如，可以在本地电脑生成一个 ssh 秘钥，看看我们呢本地电脑的代号是多少，比如：

![image-20241012224140605](../../AppData/Roaming/Typora/typora-user-images/image-20241012224140605.png)

上图中 ed25519 就是我们本地电脑的代号，在服务器端的 known_host 中把 ed25519 的行删掉（**应该是会有很多个 ed25519，导致了冲突，所以才会报这个错**）。





### 查看sshd日志

sudo journalctl -u ssh -n 100

sudo tail -f /var/log/auth.log





### 如何解决ssh经常掉线的问题：

使用tmux，就可以启用会话保持功能，但是我是debug诶，不知道可不可行







# libc.so.6误删

[关于ubuntu升级GLIBC的大坑之libc.so.6库的删除和恢复_libcso6误删除恢复-CSDN博客](https://blog.csdn.net/weixin_67874415/article/details/137187065)

[关于libc.so.6误删除紧急恢复的方案_libc.so.6 误删-CSDN博客](https://blog.csdn.net/Scirhh/article/details/84937858)

### **1. libc.so.6介绍**

/usr/lib/libc.so.6是glibc的软链接，不同的平台可能路径会不一样。
使用命令查看会看到：
[root@farmer:~]$ls -l /lib/libc.so.6
lrwxrwxrwx 1 root root 11 Jan 1 22:23 /lib/libc.so.6 -> libc-2.9.so
glibc是gnu发布的libc库，即c运行库。glibc是linux系统中最底层的api，几乎其它任何运行库都会依赖于glibc，所以说绝大部分操作命令都缺少不了它。

### 2. 误删处理（未断开ssh）

如何误删了libc.so.6，大部分系统命令将无法执行，ssh登录系统也不成功，只会无休止的提示以下错误:
error while loading shared libraries: libc.so.6: cannot open shared object file: No such file or directory
这种情况下，大部分命令已经不能执行了，只能执行例如cd,echo等小部分命令，而实用的cp,mv则不可用
经过各种百度，得到解决方法（而此种方法的前提是ssh还没断开，如果ssh已断开则无法重新连接上，得使用另外的方法用光盘重启进入急救模式）：
在同版本系统上查看/lib/libc.so.6得知是属于libc-2.9.so的软链接，因此，libc-2.9.so文件肯定还是存在的，误删的只是软链接而已，但此时想用ln命令重新建立软链接是失败的，但是可以这样强制设置变量就能执行成功！
`LD_PRELOAD=/lib/libc-2.9.so ln -s /lib/libc-2.9.so /lib/libc.so.6`
红色部分为glibc临时指定的库，这样正确执行后libc.so.6就正确恢复了。

### 3. 后续

glibc是一个非常底层的库，bash也依赖她，所以，如果把这个库干掉了，基本上啥事都干不了了，但是为啥前面设置一下LD_PRELOAD变量 就可以了呢？是这样的，LD_PRELOAD可以影响程序的运行时的链接（Runtime linker）， 它允许你定义在程序运行前优先加载的动态链接库，之前把libc.so.6这个软连接给干掉了，所以系统找不到这个库了，但是通过LD_PRELOAD设置一下glibc这个库的真实地址就可以解决这个问题了

 

通过前面设置一下LD_PRELOAD变量，后面也是可以执行其它例如cp,mv等命令的

例如我一开始不是误删，只是把libc.so.6改名了，从而也导致了上面的错误，于是就可以按照下面方法恢复libc.so.6

LD_PRELOAD=/lib64/libc-2.5.so mv /lib64/libc.so.6.bak /lib64/libc.so.6





### 如何正确升级？

[升级libstdc++、libgcc_s.so、libc.so.6 - 邶风 - 博客园 (cnblogs.com)](https://www.cnblogs.com/zhangxuan/p/10882881.html)

 



# vim编辑

按ESC键 跳到命令模式，然后输入：

:w            - 保存文件，不退出 vim
:w file  -将修改另外保存到 file 中，不退出 vim
:w!          -强制保存，不退出 vim
:wq          -保存文件，退出 vim
:wq!        -强制保存文件，退出 vim
:q            -不保存文件，退出 vim
:q!          -不保存文件，强制退出 vim

