docker可以方便环境的配置，比如`nvcr.io/nvidia/pytorch:24.05-py3` 是 NVIDIA 提供的一个 Docker 镜像，用于运行 PyTorch 框架。这个特定的镜像是从 NVIDIA 的官方镜像仓库（nvcr.io）获取的，包含了预配置的 PyTorch 环境以及必要的依赖项。



docker可以类比为一个虚拟机，但是他不是真的是一个虚拟机，它包含了运行应用所有所需要的包

在同一台机器中运行同一个docker容器，命令行中的输出在不同的终端都可以看到。

[Docker篇——Docker常用命令大全！史上最全面的Docker命令，涵盖常规命令、镜像基本命令、容器基本命令以及常用其他命令，一篇文章速通！_有docker status的命令有哪些-CSDN博客](https://blog.csdn.net/CNpeaceful/article/details/134933269)

## 向docker内的一个容器发送执行命令

docker exec <CONTAINER_ID> < xxx >

适用于docker里面有进程卡死，占用了终端无法输入命令的时候。



杀死Docker容器内的进程可以通过以下几种方式之一进行：

1. **使用`docker exec`和`kill`命令**: 如果你知道容器内部的进程ID（PID），你可以使用`docker exec`命令进入容器并使用`kill`命令来杀死进程。首先，你需要确定容器ID或者容器名称，然后使用下面的命令：

   ```
   docker exec CONTAINER_ID kill PID
   ```

   或者，如果你想要发送SIGTERM信号（这是默认的）给进程：

   ```
   docker exec CONTAINER_ID kill -15 PID
   ```

   如果你想发送SIGKILL信号（强制终止）给进程：

   ```
   docker exec CONTAINER_ID kill -9 PID
   ```

2. **使用`docker stop`或`docker kill`命令**: 如果你不知道容器内部的进程ID，或者你想直接停止整个容器，你可以使用`docker stop`或`docker kill`命令。`docker stop`会给容器发送SIGTERM信号，允许容器优雅地关闭；而`docker kill`则发送SIGKILL信号，立即终止容器。

   ```
   docker stop CONTAINER_ID
   ```

   或者，

   ```
   docker kill CONTAINER_ID
   ```

3. **通过容器的进程列表查找并杀死进程**: 如果你不确定哪个PID是你想终止的进程，你可以先列出容器内的所有进程，然后找到正确的PID。

   ```
   docker exec CONTAINER_ID ps aux
   ```

   使用上述命令找出PID后，再使用`kill`命令。

4. **编写Shell脚本自动化处理**: 如果你需要频繁地做这件事，你可以考虑编写一个Shell脚本来自动化这个过程。脚本可以包括查找容器，列出进程，选择进程，以及发送`kill`命令。

请注意，`CONTAINER_ID`应该是你的Docker容器的实际ID或者容器名称，而`PID`则是你希望杀死的进程的进程ID。在使用`kill`命令时要小心，确保你杀死的是正确的进程，以免误操作导致数据丢失或其他问题。



## 退出docker控制台

当你使用`docker attach`命令连接到一个正在运行的Docker容器时，你会进入该容器的主进程控制台。如果你想要从这个控制台安全地退出而不影响容器内的进程，可以使用以下方法：

vscode直接删掉这个终端就行了。

1. **Ctrl + P, Ctrl + Q**： 这是最推荐的方法，因为它会将控制台与容器分离，而不会向容器内的进程发送任何信号。只需按下`Ctrl + P`，紧接着按`Ctrl + Q`，你就可以退出`docker attach`会话，同时容器将继续运行。
2. **发送EOF（End Of File）**： 在大多数Unix-like系统的终端中，你可以通过按下`Ctrl + D`来发送EOF信号。这通常用于告诉程序输入已经结束。在某些情况下，这可能会关闭容器内的交互式shell，但不会终止容器的主进程。然而，这种方法不如第一种方法可靠，因为它的行为可能因容器内的应用程序而异。
3. **使用`exit`命令**： 如果你在一个交互式的shell会话中（例如，使用`bash`或`sh`），你可以简单地键入`exit`并按回车键来退出容器的控制台。这将结束shell会话，但通常不会终止容器。但是，如果容器的主进程就是这个shell，那么容器本身也会终止。

请记住，使用`Ctrl + C`通常不是一个好主意，因为它会发送一个SIGINT信号（中断信号）到容器内的进程，这可能会导致进程意外终止，除非你明确希望这样做。

总之，最安全且不会干扰容器运行的方法是使用`Ctrl + P`后紧跟`Ctrl + Q`组合键来退出`docker attach`会话。





## 查看本地docker的镜像

#### 存储位置：

当你使用 `docker pull` 命令从远程仓库拉取 Docker 镜像时，镜像会被保存到本地 Docker 守护进程的镜像仓库中。默认情况下，这些镜像会被保存在 `/var/lib/docker` 目录下。

具体的镜像存储路径如下：

```
/var/lib/docker
```

在这个目录下，Docker 会根据不同的存储驱动程序创建子目录来存储镜像和其他数据。对于镜像来说，主要的子目录是 `images`，但实际的镜像数据可能分布在多个子目录中，具体取决于你使用的存储驱动程序（如 overlay2、aufs 等）。



#### 查看镜像详细信息

如果你想要查看某个特定镜像的详细信息，可以使用 `docker inspect` 命令。例如：

```bash
docker inspect registry.cn-shenzhen.aliyuncs.com/alg orithm/keyformer:kfretail-1.0.3
```

这将输出有关该镜像的详细信息，包括其 ID 和存储位置等。



#### 注意事项

- 不建议直接访问 `/var/lib/docker` 目录下的文件，因为这些文件是由 Docker 守护进程管理和维护的。
- 如果需要更改镜像的存储位置，可以通过设置 `docker-root` 标志来更改 Docker 的存储位置，或者在 Docker 的配置文件中设置 `data-root` 参数。
- Docker 也提供了多种存储驱动程序，可以根据需要选择合适的驱动程序来优化镜像的存储。





## 查看docker容器的信息

要查看当前 Docker 容器的详细信息，包括路径映射和端口映射信息，你可以使用以下命令：

1. **查看容器的详细信息**:

   ```
   docker inspect <容器ID或容器名称>
   ```

2. **查看容器的端口映射信息**:

   ```
   docker port <容器ID或容器名称>
   ```

3. **使用 `grep` 过滤出路径映射信息**:

```
docker inspect <容器ID或容器名称> | grep Mounts -A 20
```

这里的 `-A 20` 参数表示在匹配到 `Mounts` 关键词后显示接下来的 20 行文本，这通常足以覆盖路径映射的相关信息。



## 从docker容器中复制到宿主机中

如果你只是偶尔需要保存容器内的文件数据，可以使用 `docker cp` 命令将容器内的文件复制到宿主机上：

```
docker cp <容器ID或容器名称>:/容器内的文件路径 /宿主机的目标路径
```

例如，如果想把容器内的 `/workspace` 复制到宿主机的 `/home/user/backups`：

```
docker cp <容器ID或容器名称>:/workspace /home/user/backups
```



## 打包容器为tar文件

如果需要保存整个容器的状态，可以使用 `docker export` 命令将容器导出为 tar 文件：

```
docker export <容器ID> > backup.tar
```

然后，你可以使用 `docker import` 命令将 tar 文件导入为新的镜像：

```
docker import - new-image-name < backup.tar
```

### 注意事项

- 当使用数据卷或 Docker 卷（就是`-v`路径挂载）时，请确保在容器停止或删除之后，这些卷仍然存在并且可以被重新挂载。
- 使用 `docker cp` 或 `docker export` 时，记得检查文件权限和所有者，因为这些信息可能在复制过程中发生变化。
- 如果你使用的是 Docker Compose，可以在 `docker-compose.yml` 文件中定义卷，并通过服务的 `volumes` 属性挂载这些卷。



# 使用远程镜像步骤

## 拉取远程镜像

命令：

```sh
sudo docker pull registry.cn-shenzhen.aliyuncs.com/algorithm/keyformer:kfretail-1.0.3
```

#### 命令解释：

- **`sudo`**：使用 `sudo` 来获取管理员权限，因为 Docker 通常需要 root 权限来运行。
- **`docker pull`**：这是 `docker` 命令的子命令，用于从远程仓库拉取 Docker 镜像。
- **`registry.cn-shenzhen.aliyuncs.com/algorithm/keyformer:kfretail-1.0.3`**：这是要拉取的 Docker 镜像的完整路径和标签。这个镜像来自阿里云的容器镜像仓库，名为 `keyformer`，标签为 `kfretail-1.0.3`。

#### 拉取镜像的过程：

1. **检查本地是否存在**：Docker 会首先检查本地是否有这个镜像。
2. **从远程仓库拉取**：如果没有找到，Docker 会从指定的远程仓库（这里是阿里云的容器镜像仓库）拉取这个镜像。
3. **下载镜像层**：Docker 会下载构成该镜像的所有层。
4. **组合镜像**：一旦所有层都下载完成，Docker 会将它们组合成完整的镜像。

这条命令将从阿里云的容器镜像仓库中拉取 `keyformer` 镜像，并将其存储在本地 Docker 仓库中。

#### 注意事项

- 确保你的系统能够连接到互联网，以便可以从远程仓库拉取镜像。
- 如果镜像非常大，拉取过程可能需要一些时间。
- 如果你所在的地区网络不稳定或速度较慢，可以考虑使用国内的镜像加速器来加快拉取速度。

一旦镜像被成功拉取到本地，你就可以使用 `docker run` 命令来创建并启动基于该镜像的新容器。



## 查看本地镜像

要查看当前本地所有的 Docker 镜像，你可以使用 `docker images` 命令。这将列出所有已拉取或构建的 Docker 镜像及其相关信息。

### 命令示例

```bash
docker images
```

### 输出解释

执行 `docker images` 命令后，你会看到类似下面的输出：

```
plaintextREPOSITORY                                    TAG                 IMAGE ID            CREATED             SIZE
registry.cn-shenzhen.aliyuncs.com/algorithm/keyformer   kfretail-1.0.3      123456789012        2 days ago          2.5GB
```

这里的每一列代表不同的信息：

- **REPOSITORY**：镜像的仓库名称。
- **TAG**：镜像的标签。
- **IMAGE ID**：镜像的唯一标识符。
- **CREATED**：镜像创建的时间。
- **SIZE**：镜像的大小。

### 查找特定镜像

如果你想要查找特定的镜像，可以使用 `docker images` 命令加上过滤条件。例如，要查找名为 `keyformer` 的镜像，可以使用以下命令：

```bash
docker images registry.cn-shenzhen.aliyuncs.com/algorithm/keyformer
```

### 示例

假设你想要查看是否已经拉取了 `registry.cn-shenzhen.aliyuncs.com/algorithm/keyformer:kfretail-1.0.3` 镜像，可以使用以下命令：

```
docker images registry.cn-shenzhen.aliyuncs.com/algorithm/keyformer:kfretail-1.0.3
```

如果镜像已经被拉取，你将看到类似于上面的输出。如果镜像不存在，则不会有输出。

### 注意事项

- 如果列表很长，可以使用管道 (`|`) 将输出传递给 `grep` 命令来搜索特定的镜像。例如：

  ```
  docker images | grep "keyformer"
  ```



## 创建容器

这条命令使用 `docker run` 命令来创建并启动一个新的 Docker 容器。下面是这条命令的详细解释：

```bash
sudo docker run --gpus all -itd --name my_keyformer_container --shm-size="2g" registry.cn-shenzhen.aliyuncs.com/algorithm/keyformer:kfretail-1.0.3 /bin/bash
```

#### 逐个解析命令参数：

1. **`sudo`**：使用 `sudo` 来获取管理员权限，因为 Docker 通常需要 root 权限来运行。
2. **`docker run`**：这是 `docker` 命令的子命令，用于创建并运行一个新的容器。
3. **`--gpus all`**：这个选项指定了容器可以使用所有可用的 GPU。这要求 Docker 宿主机上安装了 NVIDIA Docker 2 和相应的驱动程序。
4. `-it`：
   - `-i`：表示容器将以交互模式运行，即容器的标准输入将保持打开状态。
   - `-t`：为容器分配一个伪终端（pseudo-TTY）。 这两个选项通常一起使用，以便用户可以在容器中进行交互式操作。
5. **`-d`**：表示容器将在后台作为守护进程运行。结合 `-it` 选项，这意味着容器将以交互模式在后台运行。
6. `--name`： 指定所创建镜像的名称。
7. **`--shm-size="2g"`**：设置容器的共享内存大小为 2GB。共享内存（Shared Memory）通常用于进程间通信，提高性能。
8. **`registry.cn-shenzhen.aliyuncs.com/algorithm/keyformer:kfretail-1.0.3`**：这是要使用的 Docker 镜像的完整路径和标签。这个镜像来自阿里云的容器镜像仓库，名为 `keyformer`，标签为 `kfretail-1.0.3`。
9. **`/bin/bash`**：指定容器启动时运行的命令。这里指定了 `/bin/bash`，意味着容器启动后将进入 Bash shell。
10. `-p`： 端口映射
11. `-v`：路径映射



## 配置端口

查看端口占用情况：lsof -i （列出所有占用端口的进程，未被列出的就是没有占用）



端口配置：`6006/tcp, 8888/tcp, 0.0.0.0:8002->8001/tcp, :::8002->8001/tcp   `

要配置如上所示的端口映射，你需要在创建容器时使用 `-p` 或 `--publish` 选项来指定端口映射。下面是具体的配置方法：

#### 端口映射说明

- **6006/tcp**：将容器内的 6006 端口映射到宿主机的一个端口。
- **8888/tcp**：将容器内的 8888 端口映射到宿主机的一个端口。
- **0.0.0.0:8002->8001/tcp**：将容器内的 8001 端口映射到宿主机的 8002 端口，并允许任何 IP 地址访问。
- **:::8002->8001/tcp**：将容器内的 8001 端口映射到宿主机的 8002 端口，并允许 IPv6 地址访问。

#### 配置端口映射

在创建容器时，使用 `-p` 或 `--publish` 选项来指定端口映射。例如，如果你想为容器配置上述端口映射，可以使用以下命令：

```bash
docker run --name my_keyformer_container -p 6006:6006 -p 8888:8888 -p 8002:8001 --gpus all -itd --shm-size="2g" registry.cn-shenzhen.aliyuncs.com/algorithm/keyformer:kfretail-1.0.3 /bin/bash
```

#### 解释

- **`-p 6006:6006`**：将容器内的 6006 端口映射到宿主机的 6006 端口。
- **`-p 8888:8888`**：将容器内的 8888 端口映射到宿主机的 8888 端口。
- **`-p 8002:8001`**：将容器内的 8001 端口映射到宿主机的 8002 端口。

#### 注意事项

- 确保在创建容器时使用正确的端口号。
- 如果容器已经在运行，你需要先停止它，然后按照上述步骤创建新的容器。
- 如果你需要保留容器的数据卷，确保在创建新容器时使用相同的卷。
- 如果你有其他依赖于该容器的服务，记得更新服务配置以指向新的容器名称或端口。

通过上述命令，你可以为容器配置所需的端口映射。



## 路径映射

在 Docker 中配置路径映射通常是在运行容器时通过 `-v` 或 `--volume` 参数来完成的。路径映射允许你将宿主机上的目录映射到 Docker 容器中的目录，这样可以在容器内外共享文件。

这里是一些基本的示例说明如何进行路径映射：

#### 映射单个目录

假设你想将宿主机上的 `/home/user/data` 目录映射到容器内的 `/data` 目录，可以使用以下命令：

```sh
docker run -v /home/user/data:/data some-image
```

这里的 `-v` 参数指定了宿主机目录 `/home/user/data` 和容器内目录 `/data` 的映射关系。

#### 映射多个目录

如果你想同时映射多个目录，可以在 `docker run` 命令中多次使用 `-v` 参数：

```sh
docker run -v /home/user/data:/data -v /home/user/logs:/logs some-image
```

#### 使用匿名卷

你也可以不指定宿主机路径，让 Docker 自动管理一个匿名卷：

```sh
docker run -v /data some-image
```

#### 使用绑定挂载

如果你想更精细地控制挂载行为，可以使用绑定挂载，并指定挂载选项，例如只读挂载：

```sh
docker run -v /home/user/data:/data:ro some-image
```

这里 `:ro` 表示只读挂载。

#### 显示容器的挂载信息

如果你已经运行了一个容器，并想知道它的挂载信息，可以使用 `docker inspect` 命令：

```sh
docker inspect <容器ID或容器名称>
```

输出中会有 `Mounts` 字段，里面包含了容器的所有挂载信息。

#### 示例

假设你有一个 Nginx 容器，并且想将宿主机上的 `/opt/nginx/html` 目录映射到容器内的 `/usr/share/nginx/html` 目录，可以这样做：

```sh
docker run -d -p 8080:80 -v /opt/nginx/html:/usr/share/nginx/html nginx:latest
```

这里 `-d` 表示以后台模式运行容器，`-p 8080:80` 表示将容器的 80 端口映射到宿主机的 8080 端口。

如果你有特定的映射需求或者遇到具体的问题，请告诉我更多的细节，以便提供更精确的帮助。



## 删除容器

如果你知道容器的 ID 或者名称，可以直接使用 `docker rm` 命令来删除它。如果容器正在运行，你需要加上 `-f` 或 `--force` 选项来强制删除。

- **停止并删除容器**:

  ```sh
  docker stop <容器ID或容器名称>
  docker rm <容器ID或容器名称>
  ```

- **强制删除正在运行的容器**:

  ```sh
  docker rm -f <容器ID或容器名称>
  ```



## 查看目前存在的容器

```sh
sudo docker ps -a
```

`-a`参数表示查看所有容器（包括未运行的容器）



