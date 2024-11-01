## 远程主机配置：

### 无法连接远程主机

[解决 vscode 远程连接报尝试写入的管道不存在，ssh remote， The process tried to write to a nonexistent pipe. - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/664354803)

报错：写入管道不存在

尝试以下方案仍无法解决：

-   本地的 C:\\Users\\user\\.sshknown\_hosts 的原服务器信息全部删掉，然后重新连接
-   本地的 C:\\Users\\user\\.ssh\\config 删掉，然后重新连接
-   修改.ssh 文件的权限

这个时候，打开 vscode 的设置 File—preference-setting，将 C:\\Users\\用户名\\.ssh\config 的路径输入到 config file 下

![](https://raw.githubusercontent.com/ZZZRamsey/PicGo_save/main/202409171936359.jpeg?token=AVDP3DGWOO4HK7AHCKUUYT3G5FU6E)

<img src="https://raw.githubusercontent.com/ZZZRamsey/PicGo_save/main/202409171936374.webp?token=AVDP3DG6PIIFGPHVV44QRGLG5FU6O" style="zoom: 67%;" />

重新连接即可





网上自己租的服务器连的上，实验室的服务器就连不上。



### 安装 python 插件时，等待很久

解决办法：更换插件的版本



### 无法使用 code 来打开项目

[租用 AutoDL 服务器+使用 vscode 进行 SSH 连接+解决连接好后无法使用 code 命令打开项目（报错内容：bash: code: command not found）_linux vscode bash: code: command not found-CSDN 博客](https://blog.csdn.net/why1249777255/article/details/134296929)

解决连接好后无法使用 code 命令打开项目（报错内容：bash: code: command not found）

  **请看图：**  
![在这里插入图片描述](https://raw.githubusercontent.com/ZZZRamsey/PicGo_save/main/202409171936392.png?token=AVDP3DEQSBOVAHUCATVVKSDG5FU7K)  
  **报错原因**：该错误是因为环境变量没有加入导致的报错。  
  **参考博客**：[参考博客连接](https://zhuanlan.zhihu.com/p/638336167)，注意该参考博客的内容有点小问题，最好看我的  
  **解决办法**：看以下步骤：

-   **1、在终端输入以下命令，查看 bin 目录下的文件名字，并记住这个名字。**

```bash
ls ~/.vscode-server/bin/
```

![在这里插入图片描述](https://img-blog.csdnimg.cn/39143225382642f39f49a119ff184ab9.png#pic_center)

-   **2、在终端输入以下命令，对文件进行修改，添加环境变量。**

```bash
vim ~/.bashrc
```

  终端就会显示以下信息。  
![在这里插入图片描述](https://img-blog.csdnimg.cn/b60a441e296444de824e2da0737a84b3.png)  
![在这里插入图片描述](https://img-blog.csdnimg.cn/c03fb961730b42ec8bec491bf746a873.png)  
注意替换文件名

```bash
PATH=$PATH:~/.vscode-server/bin/2b35e1e6d88f1ce073683991d1eff5284a32690f/bin/remote-cli/
```

![在这里插入图片描述](https://img-blog.csdnimg.cn/16ac0d58f775432e83f428ad518e78bd.png)

-   **3、然后再在终端输入以下命令，更新使用修改后的配置文件**

```bash
source ~/.bashrc
```

![在这里插入图片描述](https://img-blog.csdnimg.cn/8e5b4be1b8554756b31de3fe64bf02bd.png) 
  使用 code 命令后就会弹出一个新的 VScode 界面了，可以看下图，证明 code 问题解决了。  
![在这里插入图片描述](https://img-blog.csdnimg.cn/5b6b648f07c04ce88b45cf6b55f787f3.png)



### 调试时配置 g++位置

```bash
apt install gdb
```

不需要在 launch.json 中配置 miDebuggerPath

参考：[vscode 调试出错: Unable to start debugging.The value of miDebuggerPath is invalid 问题解决-CSDN 博客](https://blog.csdn.net/aruewds/article/details/116899776)



### 无法 apt install 包

原因：没有换源

解决办法：实际上远程服务器一般会配好镜像源的，用下方指令进行查看（本地的可能要自己换源）

```bash
sudo vim /etc/apt/sources.list
```

然后只需要更新一下就行了

```bash
apt update
```



参考：[阿里云服务器 apt install 出错怎么办？出现 Package gdb is not available, but is referred to by another package 怎么办_package gcc-multilib is not available, but is refe-CSDN 博客](https://blog.csdn.net/Sansipi/article/details/121809053)



### 代码提示

VSCode 中 C/C++的函数英文文档解释，只需要安装 cpp 的插件即可，但是在 win 上没有参数的英文解释，在 linux 上才有。





## CMake 安装

ubuntu 上直接执行（版本比较老）

```bash
sudo apt install cmake -y
```

或者编译安装：

```bash
# 以v3.25.1版本为例
git clone -b v3.25.1 https://github.com/Kitware/CMake.git 
cd CMake
# 你使用`--prefix`来指定安装路径，或者去掉`--prefix`,安装在默认路径。
./bootstrap --prefix=<安装路径> && make && sudo make install

# 找到安装路径中的 bin 文件夹，在其中找到 cmake 文件，建立一个软连接(使其可以访问到)
sudo ln -s /root/bin/cmake /usr/bin/cmake

# 验证
cmake --version
```

<安装路径> 最好是个文件夹

（在 autoDL_291 上我安装到 root 上了，root 中的 CMake 文件夹是 github 克隆的项目，安装完应该可以删掉，这里没删，怕出错。）



