 CMake 学习

[【新坑预警】相信我，我真的可以把 CMake 讲清楚_哔哩哔哩_bilibili](https://www.bilibili.com/video/BV1Tw411s7Pk/?spm_id_from=333.337.search-card.all.click&vd_source=3659941460e6c74679750d458eaa5726)

C++学习路径：

1. C++
2. CMake
3. Effective modern C++
4. 多线程，模版编程
5. cuda



# CMake 在干什么？

<img src="https://raw.githubusercontent.com/ZZZRamsey/PicGo_save/main/202409171937456.png?token=AVDP3DDYLOTGI72JCNPW2KTG5FVDG" alt="image-20240208115426538" style="zoom: 33%;" />

## 解决的问题

**Linux 系统和 windows 系统编译运行流程上不统一**

写一个 CMakeList.txt 文件，CMake 会根据系统的不同帮你生成不同的 "[Makefile](# 代码编译Linux) 文件"（makefile是linux的，windows 中 vs 开发环境生成的是.sln 文件）    (第三讲 23：25)

Tip：cmake 生成的文件默认会在当前文件夹下

```bash
# 路径是CMakeList.txt文件的路径，根据不同系统生成不同的命令文件（如linux的Makefile）
# 后面的参数指的是到时候在生成可执行文件的时候，把g++都做了什么列出来。
cmake [路径] -DCMAKE_VERBOSE_MAKEFILE=ON

# --build后面跟的是build文件夹的路径，此语句可以在build下生成可执行文件
camke --build .
```



备注：

Linux用此语句生成可执行文件，window用其他的，但是cmake给统一了，下面的语句可以忘了

```bash
make
```



所以，写同样的CMakeList.txt可以让代码在不同平台编译运行，这就是CMake的跨平台特性。



---



我的理解：帮你将不同的 cpp 文件编译到一起，变成一个项目

一个厨师做菜，抛开味道不谈，至少需要知道需要什么原材料，以及这些原材料在哪。

基本配置：

```cmake
# 最低版本要求（最基本的，不写其实也就报个警告）
cmake_minimum_required(VERSION 3.10)

# 项目信息（项目名）
project(Account)

```



CMakeList.txt 也可以去找其他的 CMakeList.txt，`add_subdirectory()` 一般写在最外面的 CMakeList.txt 中，然后就可以选择具体 build 哪个文件夹。   视频 24：30

CMake 写路径，默认可以找到当前路径（配置文件所在路径）

```cmake
add_subdirectory(lesson_1)  # 去当前路径下，找lesson_1文件夹中的CMakeList.txt

add_subdirectory(./lesson_1)	# 与上面的效果一样

add_subdirectory(../lesson_1)  # 去当前路径下的上一级路径，找lesson_1文件夹中的CMakeList.txt
```



将 main.cpp 和 add.cpp 编译链接在一起，组成可执行文件 lesson_1

就是告诉厨师讲两道原材料做成一道名为 lesson_1 的菜

```cmake
# 添加可执行文件（可执行文件在哪里）
add_executable(lesson_1 main.cpp add.cpp)
```

**lesson_1 就是后面的 target**



编译运行：

1. build = 编译链接
2. 有了可执行文件就可以 执行 / debug

![image-20240207110251196](https://raw.githubusercontent.com/ZZZRamsey/PicGo_save/main/202409171937457.png?token=AVDP3DAB5XBNGLESIEGYJZDG5FVDK)





如果原材料缺少，会爆 LNK2019 错误，意味着链接错误，找不到 add 的函数体，只是声明了函数原型

<img src="https://raw.githubusercontent.com/ZZZRamsey/PicGo_save/main/202409171937458.png?token=AVDP3DBB2ZMSDSEXJPWSCKDG5FVDU" alt="image-20240207110744375" style="zoom: 50%;" />

![image-20240207110836007](https://raw.githubusercontent.com/ZZZRamsey/PicGo_save/main/202409171937459.png?token=AVDP3DAZACSFZLIBD2I3G7LG5FVDY)







# 为什么需要头文件？

## 减少重复

将函数放在头文件中统一管理

比如：当很多源代码文件引用了一个函数 add（）时，要修改函数名为 add1，就不用一个个文件去修改，直接在头文件中修改就行。



头文件只需在 cpp 文件中引入，预编译的时候就会把头文件展开到 cpp 文件中

头文件不需要在 CMakeList.txt  中 add_excutable



头文件在另外一个文件夹如何引用？

```C++
#include <../add.h>		# 头文件在上一级文件夹
```



假如有多个 cpp 文件都引用了一个头文件（在另外一个文件夹），那当这个头文件移动了，那不是所有的 cpp 文件的引用都要改？

解决（这种方法不推荐）：在某个文件夹的 CMakeList.txt 中加入

```cmake
include_directories(./lib)
```



这样这个文件夹的所有头文件都会在这个路径上去找。

# 如何将代码打包成库？

将代码打包成库，可以供自己使用，或者拱别人使用，供别人使用时，代码里面如何实现，不会暴露给别人。

## 生成静态库

1. 在要当库的文件夹的 CMakeList.txt 中，加入以下语句，**第一个参数为库名称，第二个参数是库所需的原料（.c .cpp 文件）**

```cmake
add_library(add_static add.cpp)
```

2. 然后 build，在 build 文件夹下，就在可以找到对应的 add_static **.lib**（win 系统） 文件



## 如何使用库

在要使用库的文件夹的 CMakeList 中

```cmake
target_link_libraries(test_account PRIVATE 库的绝对路径)
```



## 生成动态库

1. 和静态库同样的语句，就是多了一个 SHARED

```cmake
add_library(add_shared SHARED add.cpp)
```

2. 然后 build，在 build 文件夹下，就在可以找到对应的 add_shared **.dll**（win 系统） 文件



windows 系统上，且是用 vs 自己的编译器来编译动态库，要有特殊处理（加段语句）。			视频 20：38

此时 build 即会生成 lib 也会生成 dll，**编译的时候只会用 lib，链接的时候只会用 dll。**



dll（动态库）最好放在可执行文件同一个文件夹下，可执行文件才能执行。

放在别的地方要加系统的环境变量。



# 代码编译 Linux

## 编译流程

使用 g++ 命令对每个过程生成的文件进行排查，一般是链接出错多。

1. 预处理：对 define 定义的宏进行替换，处理 if、else 等条件编译指令，递归处理 include，生成。.i 后缀的文件（文本文档）
2. 编译：检查代码规范性和语法错误等，由编译器将代码翻译为汇编语言文件。.s 后缀
3. 汇编：由硬件将汇编语言翻译为二进制目标文件。.o 后缀
4. 链接：由链接器将二进制目标文件和与所依赖的库文件进行关联或者组装，合成一个可执行文件。



## Makefile 文件

输入 make，让系统自动帮你执行写好的命令行代码。

<img src="https://raw.githubusercontent.com/ZZZRamsey/PicGo_save/main/202409171937460.png?token=AVDP3DDCTDIYSLC3MACRUZDG5FVD4" alt="image-20240208112018363" style="zoom: 67%;" />



目标文件：所需要的文件

​		命令..

<img src="https://raw.githubusercontent.com/ZZZRamsey/PicGo_save/main/202409171937461.png?token=AVDP3DASTSJHV6IPA3PXAVTG5FVD6" alt="image-20240208111849550" style="zoom: 33%;" />



当 Makefile 找不到某个所需文件时，才会继续往下执行命令，不然后只执行第一块命令



linux 和 windows 的编译规则不一样，生成的目标文件不一样，所以是两套编译方案，但是 CMake 的出现，将两个平台统一了，所以说 CMake 是跨平台的。



# 寻找依赖 find_package

对于大部分支持了CMake的项目来说，均可以通过`find_package`找到对应的依赖库



会寻找[LibraryName]Config.cmake文件，如果在有多个opencv，那么可以在环境变量中，将想用的版本的opencv放到前面。
