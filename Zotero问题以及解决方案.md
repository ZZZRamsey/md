教程视频： [(99+ 封私信 / 81 条消息) 有梦想的小梦 - 知乎 (zhihu.com)](https://www.zhihu.com/people/meng-juan-88-22/zvideos?page=2)



[Crossref Metadata Search](https://search.crossref.org/)



# 1. 使用中出现的问题

## 插件问题





## 文献问题

### 无法抓取知网文献

无法抓取 pdf，已经尝试：

修改 dns，更新 tanslators（记得时常更新一下）

登录，多选

没办法，中文文献只能一篇一篇下载 pdf 然后拖入了



解决方案：（查看了 github 的 issue）

每次开始下载时，从 vpn 内打开知网，刷新确保已经登录，然后先进行一次手动下载，再进行插件下载。





### 参考文献引用（暂时用不到，写论文的时候需要）

[Typora+zotero 搞定 Markdown 随写随引 - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/163196155)

[使用 Zotero 在 Markdown 中优雅地处理参考文献 - 少数派 (sspai.com)](https://sspai.com/post/60825)

解决问题：用 markdown 编辑器（如 Typora）写论文时，做到与 Zotero 联动，随写随引。最后再转为 word 交给老师。

使用插件：better bibtex 和pandoc 见2.8

## 操作问题

记录一些快捷键

按住 shift 以在不同分类中移动，而不是复制



## 订阅



![img](https://pic3.zhimg.com/80/v2-a4cf246a97eb4bc719c1d2c3332f17ae_720w.webp)



<img src="https://cdn.nlark.com/yuque/0/2022/png/32594373/1662107170658-cc6aac23-b080-4b43-946e-9a3ca1c00a74.png" alt="img" style="zoom: 25%;" />



### 订阅不更新：

禁用近期安装的插件，重启 zotero 再尝试订阅







# 2. 插件使用



<img src="C:\Users\lenovo\AppData\Roaming\Typora\typora-user-images\image-20240118171906820.png" alt="image-20240118171906820" style="zoom: 67%;" />

## Zotfile

文件重命名等（可以自定义命名规则）

<img src="C:\Users\lenovo\AppData\Roaming\Typora\typora-user-images\image-20240118171924484.png" alt="image-20240118171924484" style="zoom: 67%;" />

官方网站日志：

https://zotfile.com/index.html#changelog







## better-note 知识管理（双链笔记）

### 作用

可以将各个论文中零散的笔记进行整合。可以使用 markdown

github 主页：（含有笔记模版）

: gear: [GitHub - windingwind/zotero-better-notes: Everything about note management. All in Zotero.](https://github.com/windingwind/zotero-better-notes)

官方用户指引

[0 文档简介/About (yuque.com)](https://zotero.yuque.com/staff-gkhviy/better-notes/biigg4?)



> Zotero 中的每个注释卡片可用于条目笔记中
>
> 条目笔记 == 这篇论文的笔记 （“通过注释添加条目笔记”就是将所做的注释全部添加进条目笔记，除了手写的注释）
>
> 主笔记 == 整理条目笔记的笔记

如果用卡片笔记法理解的话，平时 zotero 自带的功能里创建的每一条笔记都是一张卡片，而所谓的“主笔记”就是一个整理卡片的盒子，通过放置卡片的链接而达到收纳功能。这也是为什么 up 主说她不在主笔记里写很多东西，“主笔记”只是起到收纳功能而已。这个插件的功能和 obsidian 很像，但是更强大之处在于，zotero 本身具备整理文献、收集文献信息的功能，所以通过这个笔记插件可以达到输入与输出同步进行，且数据共享的效果，比如可以直接插入文献引用数据。[^1]

[^1]: [Zotero超级好用的笔记软件zotero better notes ，较详细操作教程与小白指南。内含笔记模板制作方法1_哔哩哔哩_bilibili](https://www.bilibili.com/video/BV1Fg411H7ZH/?spm_id_from=333.337.search-card.all.click&vd_source=3659941460e6c74679750d458eaa5726)



### 笔记模版

笔记模版，在 github 主页的 issue 中

[Zotero 的 zotero-better-notes 支持自定义笔记模板，欢迎大家分享好用的模板_哔哩哔哩_bilibili](https://www.bilibili.com/video/av214333267/?vd_source=3659941460e6c74679750d458eaa5726)

[4.1 双链笔记/Bi-directional Link (yuque.com)](https://zotero.yuque.com/staff-gkhviy/better-notes/yxpiew)





## Markdown Here

在笔记中，选中要渲染的部分，按“Ctrl+Alt+M”进行 markdown 渲染





## Zotcard

一个方便建立卡片的软件，方便定义各种模版卡片，这可以作为条目笔记或者作为注释

注意修改每个卡的名字，以区分，并且讲这些不同的名字设为同一个标签

[一个很详细的笔记模版，包含询问 chatgpt 的句子](https://github.com/018/zotcard/discussions/2#discussioncomment-5954035)



## Zotero IF 

重启 Zotero 后调出“馆藏目录”和“索取号”，分别对应中科院分区和影响因子（JCR IF ==只针对 SCI 期刊论文==）



## zotero-doi-manager

该插件自动获取期刊文章的 DOI 名称，以及使用 http://shortdoi.org 查找 shortDOI 名称。该加载项还会验证存储的 DOI 是否有效，并标记无效的 DOI。

插件功能：

- 获取 shortDOI：对于所选项目，查找 shortDOI（替换存储的 DOI，如果有）并标记无效的 DOI。
- 获取长 DOI：对于所选项目，查找完整的 DOI（替换存储的 DOI，如果有）并标记无效的 DOI。
- 验证并清理 DOI：对于所选项目，查找完整的 DOI（替换存储的 DOI，如果有），验证存储的 DOI 是否有效，并标记无效的 DOI。
- 此函数还会从 DOI 字段中删除不必要的前缀（如：发布者 URL 前缀）。



原文链接：https://blog.csdn.net/qq_43309940/article/details/117126357

[什么是 DOI？如何获取文献的 DOI？ - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/147494557)



## Zotero Scholar Citations

因为要访问 google， 所以要科学上网才能更新引用数，或者改源码，使其访问国内镜像，如下：

[在国内使用Zotero Scholar Citations插件 - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/50789047)



==国内谷歌学术镜像==：[谷歌学术 (99lb.net)](https://gfsoso.99lb.net/scholar.html)



## better bibtex

用markdown编辑器写论文时，方便进行文献引用，配合pandoc转为word格式

[案例](http://47.98.142.167/238/)





## 使用Zotero当作ppt笔记软件

禁用Zotfile（重命名），scihub，茉莉花（自动寻找对应文献）

取消了高亮自动翻译。
