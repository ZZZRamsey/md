官方说明：https://support.typora.io/Markdown-Reference/

b站视频链接：

https://www.bilibili.com/video/BV1JA411h7Gw/?spm_id_from=333.337.search-card.all.click&vd_source=3659941460e6c74679750d458eaa5726

Markdown 语法参考 : https://www.runoob.com/markdown/md-tutorial.html
表情全部名称：https://unicode.org/emoji/charts/full-emoji-list.html

---

[张一鸣的150条深度思考，坚决告别惰性！ - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/607848325)



---

<details>
<summary>样例</summary>
    sadaidjsiadjisadj
</details>

[(16条消息) Markdown展开与收起的黑三角_markdown收起展开_509728263的博客-CSDN博客](https://blog.csdn.net/u014171091/article/details/112696798)



---

各种箭头，Letex代码（用$$包裹住）

[(16条消息) Latex各种箭头符号总结_latex箭头_邱之涵0的博客-CSDN博客](https://blog.csdn.net/Artoria_QZH/article/details/103310704)





typora小插件

[GitHub - obgnail/typora_plugin: Typora plugin. feature enhancement tool | Typora 插件，功能增强工具](https://github.com/obgnail/typora_plugin)

更新后打开文件是空白的：移除plugin文件夹，并且重新下载一个来，再把plugin复制进去

everything搜索

typora_plugin-1.7.35







链接标题：

语法：

![Typora编辑器如何添加内部链接](https://exp-picture.cdn.bcebos.com/3852f6e5eceeadbc757597c5cd18dfdae53b7bf0.jpg?x-bce-process=image%2Fresize%2Cm_lfit%2Cw_500%2Climit_1%2Fformat%2Cf_auto%2Fquality%2Cq_80)

ctrl加鼠标右键，即可跳到所链接的标题处。

删除线：~~两个波浪号包裹~~



更改快捷键：

[1.#_3 Typora(markdown格式文本编辑器) -- 配置高亮及快捷键_markdown高亮-CSDN博客](https://blog.csdn.net/qq_43529621/article/details/106572442)

高亮快捷键：ctrl+q





## 图片问题：

使用图床上传图片，图片在Typora不显示

[picgo使用github做图床，图片在相册不显示，在github上也无法查看_picgo相册里显示不了图片-CSDN博客](https://blog.csdn.net/ZMMMOO/article/details/127270446)最近整合picgo + github 弄图床，弄了好久终于上传成功了，但是发现相册里面没有图片都是空的

也无法打开查看

网上找了好久，找寻各种答案：
1.重启picgo
2.重新安装picgo
3.配置代理等等
终究无法解决
原因竟然是上传到github的图片链接（https://raw.githubusercontent.com/xxxx.png）这玩意压根就不能访问—GitHub的raw.githubusercontent.com域名解析因为某种不可描述的原因给污染了，不相信的小伙伴可以试一试哈

好了好了，下面开始真正解决！！！

在https://www.ipaddress.com首页搜索raw.githubusercontent.com，查询真实的ip地址，这四个随便选一个就行，不放心可以自己先在小黑窗口ping一下

鼠标右键点击桌面左下角的开始菜单，选择Windows PowerShell（管理员）
在打开的 窗口中输入notepad, 回车, 会打开记事本
选择文件 -> 打开
在弹出的文件选择窗口中, 选择 C:\Windows\System32\drivers\etc\hosts
在最底下添加该内容即可
185.199.108.133 raw.githubusercontent.com

其实这样保存后就ok了，不放心就刷新一下dns—在小黑窗口（win+r -> cmd -> ipconfig/flushdns -> 回车）
如果对您有帮助请收藏起来，跟朋友装杯，用这种方法还可以改github访问速度（改ip）!!!
————————————————

原文链接：https://blog.csdn.net/ZMMMOO/article/details/127270446





## github上的markdown

[解决github或gitee上传的md文件中TOC标签无法生成目录_gitee markdown toc-CSDN博客](https://blog.csdn.net/Grantr/article/details/113740887)

[github上如何为markdown文件生成目录 - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/126353341)
