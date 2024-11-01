# jupyter插件

jupyter扩展插件安装：

[miniconda环境搭建和Jupyter Notebook入门使用-CSDN博客](https://blog.csdn.net/m0_73678713/article/details/133795098)



注意插件仅支持7以下的notebook版本

[【jupyter notebook中插件 nbextensions 安装失败分析与解决方法】_no module named 'notebook.base-CSDN博客](https://blog.csdn.net/weixin_54383080/article/details/134655727#问题描述)

在卸载旧版本的 Jupyter Notebook 并安装另一个版本的 Jupyter Notebook 时，通常不会导致与现有的 Jupyter Lab 冲突。Jupyter Lab 和 Jupyter Notebook 是独立的应用程序，它们之间没有直接的依赖关系。您可以在同一系统上安装不同版本的 Jupyter Notebook 和 Jupyter Lab，并且它们应该可以正常共存。



## 目前conda环境说明

目前py3.8那个环境是同时存在不同版本的jupyterlab和notebook

test_env是配置好notebook的环境

kaggle是test_env的复制

[Jupyter Notebook和NBextensions插件安装使用教程_哔哩哔哩_bilibili](https://www.bilibili.com/video/BV1Q84y1L7XG/?spm_id_from=333.1007.top_right_bar_window_history.content.click&vd_source=3659941460e6c74679750d458eaa5726)



## 扩展使用教学

[jupyter notebook 使用方法 (06) - 使用nbextensions扩展功能和修改界面风格_哔哩哔哩_bilibili](https://www.bilibili.com/video/BV1uL411P7HK/?spm_id_from=333.788.recommend_more_video.1&vd_source=3659941460e6c74679750d458eaa5726)



# jupyter启动

要在miniconda的python环境中启动jupyte-notebook和jupyter-lab



- 为什么会打开pycharm？？

因为使用了错误的打开命令行命令

正确的应该是：```jupyter-notebook```



- jupyter为什么会打开word？

配置jupyter环境变量×

配置一个默认的浏览器就解决了（设置chrome还是会打开word，只能设置edge，但是把链接复制到chrome中也能用）

[给jupyter notebook 设置默认打开的浏览器操作_哔哩哔哩_bilibili](https://www.bilibili.com/video/BV1LG4y157hF/?spm_id_from=333.337.search-card.all.click&vd_source=3659941460e6c74679750d458eaa5726)





# jupyter使用

以下是Jupyter Notebook的常用快捷键：

- 进入命令模式：按esc键
- 进入编辑模式：按enter键
- ==在命令模式下，按A键可以在当前单元格上方插入新单元格，按B键可以在当前单元格下方插入新单元格==
- 在命令模式下，按D键两次可以删除当前单元格
- ==在命令模式下，按M键可以将当前单元格转换为markdown格式，按Y键可以将当前单元格转换为代码格式==
- 在命令模式下，按shift + enter键可以运行当前单元格并跳转到下一个单元格
- 在编辑模式下，按ctrl + /键可以注释当前行或取消注释
- 在编辑模式下，按shift + tab键可以查看当前函数的用法
- ==ALT + 鼠标左键：多行编辑==
- Shift + Tab：显示函数/方法的帮助信息（智能提示）
- Ctrl + A：全选
- Ctrl + X/C/V：剪切/复制/粘贴
