[Anaconda conda常用命令：从入门到精通_conda命令-CSDN博客](https://blog.csdn.net/chenxy_bwave/article/details/119996001)

  

```bash
conda create --name target_env_name --clone source_env_name
```

注意这条指令，target_env_name是要创建的环境的名字，source_env_name是被复制的环境，创建的环境不会重新下载源环境中已存在的包，而是使用链接的方式。



---



环境的复制迁移（失败）

1. 有些包例如torch，无法直接下载
2. 包之间有冲突，失败ERROR: ResolutionImpossible: for help visit https://pip.pypa.io/en/latest/topics/dependency-resolution/#dealing-with-dependency-conflicts



[备份、压缩、复制现有conda环境 - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/666745604)





环境迁移：

 [【conda】实现conda环境迁移的4种方式_conda环境移植-CSDN博客](https://blog.csdn.net/baidu_35692628/article/details/136519579) 

