[TOC]

# 序章

: fist_oncoming: 李沐论文精读系列

: cowboy_hat_face: author：Ramsey Zhu

## 相关网址链接

: video_camera: [YouTube](https://www.youtube.com/@mu_li)

: video_camera: [bilibilil](https://space.bilibili.com/1567748478/channel/collectiondetail?sid=32744)

: star: [github]([mli/paper-reading: 深度学习经典、新论文逐段精读 (github.com)](https://github.com/mli/paper-reading))

(github 中有论文下载地址)

## 相关笔记链接

[「课代表来了」跟李沐读论文之——BERT - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/449787826)

[「课代表来了」跟李沐读论文之——Transformer - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/447239102)







## 读论文方法论？

原视频：[如何读论文【论文精读· 1】_哔哩哔哩_bilibili](https://www.bilibili.com/video/BV1H44y1t75x/?spm_id_from = 333.999.0.0&vd_source = 3659941460e6c74679750d458eaa5726)

* 第一遍读的目的就是为了筛选论文，从茫茫大海之中捞出你需要的那根针。我们都知道一旦做学术研究那方向便是非常细分的，有很多看起来和你沾边的文章实际上对你的工作并无帮助，如果对这些文章也进行精读那成本是很高的。因此第一遍读就只读 **标题（title）、摘要（abstract）和结论（conclusion）**。读标题可以迅速圈定范围，即这篇文章是不是和我的工作相关；摘要主要简单介绍一下论文在做什么；结论同摘要类似，一般换几个单词换一种说法，列几个关键数字证明我的工作如何如何牛逼。读完这三部分，实际上一篇文章大体在讲什么你心中就有数了。当然，这第一遍读还没完，你还需要跳到论文的实验部分，去看看图片、表格，看看他们做了啥写了啥。实际上这也符合人类的认知，人总是第一眼对图片印象深刻，图片这种具象化的东西实际上往往也承载着作者将 ==抽象思维具象化的过程==，因此很容易就能获取更多有价值的信息。这第一遍读下来，往往十几分钟的时间，但是你就能对一篇文章有了一个通盘的把握。**第一遍，目的是就是为了了解哪些文章对我是重要的，这决定了你是否还要再继续读下去。**

* 第二遍读就要对整个文章过一遍，要知道每一部分在干什么。不过这一遍也不用太注意细节，尤其是一些公式推导、证明之类的，往往这些一个地方就能耗你一两天才搞明白，但这在第二遍读的时候是得不偿失的。但是，不是说第二遍不用关注细节了，第一遍你瞄了一眼的图表，此时就需要一个字一个字弄清楚作者是怎么做的，<mark> 算法流程图 </mark> 里面是怎么一步步实现的，作者提出的算法和原有方法之间有什么区别，改进在何处。可能这一遍读还是不太能搞清楚论文的具体逻辑，尤其是对于刚进入一个领域的新人来说，但至少你熟悉了很多这个领域的专有名词，你可以去查阅每个 <u> 名词 </u> 的意思，帮助你更好地理解这篇文章。同时，这一遍阅读你也会注意到一些经典的文献，这些被引用的文献很多都是该领域的奠基之作或有重大影响力的论文，这些论文就值得你圈出来，去用之前读第一遍的方式浏览一下。**第二遍读，目的就是厘清文章脉络，知道在讲什么、怎么做的、做的怎么样，同时也决定你是否要读第三遍。**

* 第三遍既是最后一遍也是最详细的一遍，在这一遍里李沐老师的要求是搞懂论文每一句话在干什么。在读文章的时候你就要以文章作者的视角去读，我该如何解决这个目前的问题，我该如何设计这个实验，如何对现有方法进行改进。甚至文章最后作者说还有哪些展望，你也可以想想换做是自己能不能继续做下去。第三遍读方法论最少，但实际上要求最高，要能对整篇文章达到一个烂熟于心的水平，让你去做这篇文章的分享，几乎能抵挡得住来自四面八方的提问。要能在合上文章之后脑海里清晰浮现每一个细节和难点，只有这样才能算真正读懂。**第三遍读，就在于真正读懂。**



# 论文

## AlexNet

作者：Alex，IIya，Geoffrey

- 题目：**用深度卷积神经网络进行 ImageNet 分类**
- 摘要 ：**我们训练了一个很大的深度卷积神经网络来实现 ImageNet 分类，结果优于之前所有工作。怎么做的呢，他有庞大的模型结构和变量，自然需要解决速度和过拟合的问题。1.用了 ==非饱和神经元== 和 GPU 使训练加速**（2012 年 GPU 不算最新，08 年推出的 CUDA2.0，但不可否认是当时的亮点）**2.用最新开发的正则化方法叫 “dropout”来减少过拟合。**
- 介绍 **：目前物体识别的方法主要是机器学习，收集更大的数据，学习更强的模型，使用更好的技术，正则，减少过拟合**（神经网络之前的大数据时代就是这么处理的，李沐老师说如今正则也没那么重要，如何更好的设计一个网络才更重要。） **直到现在有标注的数据集相对于数以万计的图像，而现实却需要很大的数据集，现在已经可以有这样的数据集了，例如 LabelMe 和 ImageNet 。即使像 ImageNet 这样大的数据集也无法解决物体检测这样大的复杂任务，所以我们用了一些经验之谈以弥补缺失的数据，cnn 就是这样的模型，可以根据高宽控制他的容量，他也对图片的本质做了强有力的，基本正确的假设。因此与有相似大小层数的前馈神经网络相比，cnn 有更少的连接参数更容易训练，并且比他理论情况的最小值稍低一点点。**（李沐老师说引言一般讲故事，我在做什么，那个方向，研究现状怎么样，我们怎么做，为什么重要，别人怎么做。当时主流模型并不是 cnn，我们写的时候最好提一下，别人的比较一下。）**尽管 cnn 足够优秀但是应用于大规模超分辨率依然成本高昂，但是 GPU+高度优化的 2D 卷积的实现足以应对，标签重组的 ImageNet 也能减少过拟合。我们特殊贡献如下：ImageNet 子集上训练了迄今为止最大的卷积神经网络之一，并在比赛中取得了最好成绩，我们编写了搞笑的 GPU 来实现 2d 卷积，并且在训练 cnn 时候其他内在操作，我们将公开。我们的网络包含了一些新的非同寻常的特征提高了他的表现和减少了训练时间。即使有 120 万个有标注的训练样本，我们的网络太大了使过拟合是个问题，所以我们采取了很多有效的办法来避免。我们最后的网络包括 5 个卷积层和 3 个全连接层，丢在任何一层都是性能更差**（这个结论存疑）**最后，网络的大小取决于我们目前 GPU 的可用内存大小和我们能忍受的训练时间。我们的网络在两块 GTX 580 3GB GPUs 上训练了五六天。我们所有的实验表明，只要有更快的 GPU 和更大的数据集出现，我们结果更好**（现在看来是废话是因为我们认同了这个真理，更说明在当时情况 Geoffrey 团队的先见之明。）
- 数据集：**除了裁剪之外没做其他预处理，在原始 RGB 上训练的网络。**（李沐老师讲端到端 end to end，即原始的图片，原始的文本进去就能进行训练，算一个优势，但是当时 ALex 等人并没有把他当作卖点，可能没意识到。其余是介绍了一下 ImageNet 略）
- 网络架构：**8 个学习层，包括 5 个卷积层和 3 个全链接，根据重要顺序先后介绍。**
  1. **ReLU 非线性函数：一般用 tanh 或者 sigmoid。就梯度下降的时间而言，==饱和的非线性函数比非饱和的非线性函数例如 f(x) = max(0, x)训练慢很多，我们把有这非线性特性的神经元成为 Rectified Linear Units (ReLUs)。== ReLU 要好于 tanh，图中展示了在 CIFAR10 数据集上，对于特定的四层卷积网络，将错误率下降到 25%所需要的迭代次数，图中表明，如果继续用传统的饱和神经元，我们根本无法完成如此大的模型的训练。**（图中显示 ReLU 快 7 倍，没有说为什么快）**也有很多研究要替代传统非线性函数，但是他们对新数据集的适应能力没有 ReLU 好。**（现在来看当其他技术加入时，ReLU 并没有快多少，用他是因为简单，简单就是胜利。aaaa，why haven't I finished translating! fidget！surely it doesn't mean that I am too worried...another day passed away，set up a flag: finish the work today！）


1. **在多个 GPU 上训练：一块 GTX 580 GPU 算力不够，结果表明，120 万个训练样本足够训练一个此 GPU 无法容量的大网络，因此我们对此网络划分了两个 GPU，目前的 GPU 有两好的跨块通信能力，而不需要通过主机内存。我们讲网络切一半分给每个 GPU，还有一个技巧：仅仅某些层有 GPU 通信。**（看原来的网络结构也能知道，有的层在分 GPU 训练，有的层还要通信，可乱了，目的是什么，为什么称之为技巧，还没理解。李沐老师说这都是当时工程上的事情，在之后 GPU 发展起来，这些技术不太重要，但是，风水轮流转，现在 nlp 兴起，需要训练的数据更大更大了，分 GPU 又成了可行之道。）

2. **本地响应正则化：: star: <mark> ReLU 有个很好的特性，不需要输入归一化来防止饱和，只要有输入，神经元就开始学习，但是我们仍然发现一下局部归一化有助于泛化 </mark>**（<u> 这是 ReLU 的优点，其实也是缺点，因为不同于线性激活函数，ReLUs 每一次学习都是不可逆的，有时候让网络什么事都不干也是一件挺难得事情，后面 ResNet 实现了什么的知乎文中讨论了这样的事情 </u>）MobileNet V2 [^2] 的论文也提到过类似的现象，由于非线性激活函数 Relu 的存在，每次输入到输出的过程都几乎是不可逆的（信息损失）。我们很难从输出反推回完整的输入。

3. : question: **[最大池化重叠](https://www.zhihu.com/search?q=重叠池化)：cnns 中的池化层在同一内核映射相邻神经元的输出，一般来说由临近的池化神经元汇总成的邻域是不重叠的，更准确的说，每个池化层可以被理解成由间隔 s 像素的池化神经元网格组成，以池化神经元的位置为中心组成 z\*z 的邻域，如果我们设置 s = z，就得到传统的通常在 cnn 中使用的原始池化层，如果设 s < z，就得到重叠池。我们 s = 2 z = 3。**

4. **总体架构：网络包含 8 个带权重的层，前 5 层是卷积剩下的 3 层是全连接，最后一个全连接的输出使用了 softmax，输出 1000 个分类标签.我们的网络最大化了多项逻辑回归目的，这相当于最大化了预测分布下正确标签的对数概率跨训练案例的平均值。**（这句话没读懂，之后描述了具体模型架构，主要最后全连接的输出都是 ReLU，每个层用的卷积核和输出，并且是直接在 256 的原始图像上操作）。

5. **模型并行**：把模型切开使之能训练，当时这个技术提出来并没有引起多大的关注，实际上把模型实现好一点也能训练。但是近两三年在自然语言处理领域，有 100 亿，1000 亿的模型，发现训练不动，人们才想到这个方法的可贵之处。

- 减少过拟合（不是本文做的工作）：首先是两种数据增强的方法，第一种方法是在图上随机抠下来一个比较小的区域，一张图有很多种抠法。第二种方法是在 RGB 通道上做一点改变，用的是 PCA（主成分分析）。然后是 Dropout，这个方法用于解决多个模型融合过于费时的问题，以 50%的概率随机的把一些隐藏层的输出变为 0，而且这些被 Dropout 神经元都不参与前向传播和反向传播，这样每一次都能的到新的模型，但是这些模型没有设为 0 的权重都是共享的，等价于实现了模型的融合。（: question: 现在认为 [Dropout](https://www.zhihu.com/search?q=Dropout) 只是一个正则项，在现行模型上的效果等价于一个 L2 正则项）
- 讨论：**我们的结论是，一个很大的深度卷积神经网络具备在有挑战性的数据集上用纯监督式学习实现破纪录式结果的能力**（他想说两点，deepcnn 很强，纯监督式导向）。**我们没有用无标签图像预热网络（他还是倡导有监督帮派嘛，确实这是一个监督分水岭，之前无监督之后有监督，李沐老师说，如今 nlp 中无监督又回到主流），只要网络够大训练时间够久结果就越好**（他这句话在如今看就是废话，但是当时不是。至少他得到了一个非常肯定的结论，网络越大越好，这可以推出，硬件越牛越好，也可以近似等于，以后哪家机构越有钱，结果越好，，，科研实力+金钱实力。15 年的 ResNet 证明，事实并非如此，但是有“残差”的办法使得越来越深越来越大效果还不错，，，，当我没考上比较好的机构的时候，人工智能瓶颈就到了。每日一 emo，emo 结束，继续搬砖）。**网络虽然在图像识别做的不错但是和人的能力差很远**（现在已经远超人了）。**我们希望在视频序列中用很深的网络训练，因为时序包含了一些信息是静态图片没有的**（他提出图像识别之后的工作-视频，但是 video 计算量远大于图像所以直到今天还没有解决，这里可以探索更强的算力，或者更好的算法。加之 video 版权更复杂，所以直到今天也没有很好的发展。但是！在那个时候就已经想到了 video 领域，牛啊牛啊）





## Resnet

作者 Kaiming He Xiangyu Zhang Shaoqing Ren（在蔚来居然） Jian Sun（导师）

Microsoft Research (MSRA 微软亚洲研究院)

**摘要**：

我们提出一个网络，他可以简化网络的训练，这些网咯整体上比以前深得多。我们显示的用带有与输入层的关系的残差机制重新制定这些层，而不是去学习没有关系的函数。我们提供了全面的经验证据来表明这些 [残差网络](https://www.zhihu.com/search?q=残差网络&search_source=Entity&hybrid_search_source=Entity&hybrid_search_extra={"sourceType"%3A"article"%2C"sourceId"%3A"587284929"}) 更容易被优化，并且，可以在很深的网络获得准确率。我们用很深的层数，比 VGG 要深 8 倍，但是依然有更低的复杂度。这些残差网络的集合在 ImageNet 网络上的获得了 3.57 的错误率。在 2015 分类任务上第一名，我们还在 100-1000 层上做了分析。

表征深度对很对视觉识别任务都至关重要，仅仅因为我们极端的表征深度，我们就在 coco [目标检测](https://www.zhihu.com/search?q=目标检测&search_source=Entity&hybrid_search_source=Entity&hybrid_search_extra={"sourceType"%3A"article"%2C"sourceId"%3A"587284929"}) 数据集上获得了 28 个百分点的提升。[深度残差](https://www.zhihu.com/search?q=深度残差&search_source=Entity&hybrid_search_source=Entity&hybrid_search_extra={"sourceType"%3A"article"%2C"sourceId"%3A"587284929"}) 网络是我们提交给这些竞赛的基础，在这些竞赛中，我们在检测，定位，分割上获得了第一名。



**论文试图解决什么问题**：

解决深层神经网络即使收敛之后比对应的浅层网络正确率更差的问题。

* **resnet 为什么能叠加到一千层，传递损失不大嘛**？

首先，搞懂之前的网络为什么不深，如果很深会出现什么问题。随着网络的加深，会有梯度消失或者爆炸的问题，因为乘法的求导造成，之前一般用正则和 Bacth Normalization(简称 BN，归一化)解决这个问题，解决之后面临新的问题就是衰退，深层网络的正确率反而劣于浅层网络，为了解决这个问题，作者提出了残差网络，学习残差。设下层输出为 h(x)，上层输出为 x，下层主要任务是拟合 f(x)= h(x)-x，所谓残差。这样，下层输入变成了 f(x)+x，至少保证 x 不变。

<img src="https://pic3.zhimg.com/v2-f21af11f6e7e3def5202b31cb0d2952e_b.jpg" alt="img" style="zoom: 33%;" />



* **resnet 为什么一定比 shallow 不差**

大不了残差映射权重为 0，x 是恒等映射。



* **resnet 的亮点是什么**

残差，f(x)+x 的维度统一的处理



* **介绍 resnet 的 short connections**

x 学习到的内容不变直接传到下一层，物理上的短路链接 ，很形象，深度残差网络速度快也是因为此，短路的时候传播很快。



* **resnet 的 [网络退化现象](https://www.zhihu.com/search?q=网络退化现象&search_source=Entity&hybrid_search_source=Entity&hybrid_search_extra={"sourceType"%3A"article"%2C"sourceId"%3A"587284929"}) 是过拟合嘛 是梯度消失吗，那是什么**

不是过拟合，因为文中实验给出，训练集也变差所以不是过拟合。也不是的梯度消失因为他可以收敛。是一种新的，层数变深，误差在训练集测试集都增大的实验现象。



* **resnet 的残差 f(x)和 x 相加为拟合目标函数 h(x)的过程中，x 和 f(x)维度不同如何处理, resnet 的 1x1 卷积目的**

一种是使用 zero padding(不增加参数量)，另一种是维度不同的时候使用 1 × 1 的卷积核作投影，步长为 2 来改变维度(增加参数量)同时高宽不变，第三种是不管维度是否一样，都做投影。实验效果第三种最好，第二种差不了多少，作者选用第二种，考虑了计算复杂度。

<img src="https://pic2.zhimg.com/v2-f8061fb737dba155d23f407b73388f01_b.jpg" alt="img" style="zoom: 50%;" />

TODO: 待更新，3.2Identity Mapping by Shortcuts 没看懂。且涉及 he 的另一篇论文

* **resnet 如何解决梯度消失问题，为什么 resnet 收敛的比较快**

1. f(x)这个正向传播的残差可能会很小，plainnets 梯度消失就是出现在一层一层的正向传播权重太小，而 f(x)+x 加的 x 为短路链接，不用正向传播，直接相加，它不会变小。其实和 plainnets 解决梯度消失的方法类似，正则化不过也是赋值权重+一个大值。

2. shortcut connection 相当于高速直通公路



### **一、引言：为什么会有 ResNet？ Why ResNet？**

> 神经网络叠的越深，则学习出的效果就一定会越好吗？

答案无疑是否定的，人们发现当模型层数增加到某种程度，模型的效果将会不升反降。也就是说，深度模型发生了退化（degradation）情况。

那么，为什么会出现这种情况？

#### **1. 过拟合？ Overfitting？**

首先映入脑海的就是 Andrew Ng 机器学习公开课 [^1] 的过拟合问题



<img src="https://pic1.zhimg.com/80/v2-0fd6590cfa7d9cd57955647b8a07f1e3_720w.webp?source=1940ef5c" alt="img" style="zoom:80%;" />

Andrew Ng 的课件截图

在这个 [多项式回归](https://www.zhihu.com/search?q=多项式回归&search_source=Entity&hybrid_search_source=Entity&hybrid_search_extra={"sourceType"%3A"answer"%2C"sourceId"%3A786270699}) 问题中，左边的模型是欠拟合（under fit）的此时有很高的偏差（high bias），中间的拟合比较成功，而右边则是典型的过拟合（overfit），此时由于 **模型过于复杂**，导致了高方差（high variance）。

然而，很明显当前 CNN 面临的效果退化不是因为过拟合，因为过拟合的现象是 "高方差，低偏差"，即测试误差大而训练误差小。但实际上，深层 CNN 的训练误差和测试误差都很大。

![img](https://picx.zhimg.com/80/v2-d3aeddd94cb963176d7154485cdac17c_720w.webp?source=1940ef5c)

（a）欠拟合与过拟合 （b）模型退化

#### **2. 梯度爆炸/消失？ Gradient Exploding/Vanishing？**

除此之外，最受人认可的原因就是“梯度爆炸/消失（弥散）”了。为了理解什么是梯度弥散，首先回顾一下反向传播的知识。

假设我们现在需要计算一个函数 f(x, y, z)=(x+y)× zf(x, y, z)=(x+y) \times  zf(x, y, z)=(x+y) \times  z ， x = − 2x =-2x =-2 , y = 5y = 5y = 5 , z = − 4z =-4 z =-4 在时的梯度，那么首先可以做出如下所示的计算图。

将 x = − 2x =-2x =-2 , y = 5y = 5y = 5 , z = − 4z =-4 z =-4 带入，其中，令 x+y = qx+y = q x+y = q  , 一步步计算，很容易就能得出 f(− 2,5, − 4)= − 12f(-2,5,-4)=-12 f(-2,5,-4)=-12  。

这就是前向传播（计算图上部分绿色打印字体与蓝色手写字体），即：

<img src="https://picx.zhimg.com/80/v2-7a18c5ddfe506b297b550c82b0dfef27_720w.webp?source=1940ef5c" alt="img" style="zoom:67%;" />

前向传播是从输入一步步向前计算输出，而反向传播则是从输出反向一点点推出输入的梯度(计算图下红色的部分)。

<img src="https://pic1.zhimg.com/80/v2-9d807b3001b8ef51aa7196dc939ee888_720w.webp?source=1940ef5c" alt="img" style="zoom:67%;" />

<img src="https://picx.zhimg.com/80/v2-ea3c10b38025b21d401ef3634d9671b1_720w.webp?source=1940ef5c" alt="img" style="zoom:67%;" />

原谅我字丑……

注：这里的反向传播假设输出端接受之前回传的梯度为 1（也可以是输出对输出求导 = 1）

观察上述反向传播，不难发现，在输出端梯度的模值，经过回传扩大了 3~4 倍。

这是由于反向传播结果的 **数值大小** 不止取决于求导的式子，很大程度上也取决于 **输入的模值。** 当计算图每次输入的模值都大于 1，那么经过很多层回传，梯度将不可避免地呈几何倍数增长（每次都变成 3~4 倍，重复上万次，想象一下 310000 有多大……），直到 Nan。这就是梯度爆炸现象。

当然反过来，如果我们每个阶段输入的模恒小于 1，那么梯度也将不可避免地呈几何倍数下降（比如每次都变成原来的三分之一，重复一万次就是 3-10000），直到 0。这就是梯度消失现象。值得一提的是，由于人为的参数设置，梯度更倾向于消失而不是爆炸。

由于至今神经网络都以反向传播为参数更新的基础，所以梯度消失问题听起来很有道理。然而，事实也并非如此，至少不止如此。

我们现在无论用 Pytorch 还是 Tensorflow，都会自然而然地加上 Bacth Normalization(简称 BN)，**而 BN 的作用本质上也是控制每层输入的模值，** 因此梯度的爆炸/消失现象理应在很早就被解决了（至少解决了大半）。

不是过拟合，也不是梯度消失，这就很尴尬了……CNN 没有遇到我们熟知的两个老大难问题，却还是随着模型的加深而导致效果退化。无需任何数学论证，我们都会觉得这不符合常理。等等，不符合常理……

#### **3. 为什么模型退化不符合常理？**

按理说，当我们堆叠一个模型时，理所当然的会认为效果会越堆越好。因为，假设一个比较浅的网络已经可以达到不错的效果，**那么即使之后堆上去的网络什么也不做，模型的效果也不会变差**。

*然而事实上，这却是问题所在。“什么都不做”恰好是当前神经网络最难做到的东西之一。*

MobileNet V2 的论文 [^2] 也提到过类似的现象，由于非线性激活函数 Relu 的存在，每次输入到输出的过程都几乎是不可逆的（信息损失）。我们很难从输出反推回完整的输入。

<img src="https://pic1.zhimg.com/80/v2-e0e43e18c61a82e24e5a837740843963_720w.webp?source=1940ef5c" alt="img" style="zoom: 67%;" />

Mobilenet v2 是考虑的结果是去掉低维的 Relu 以保留信息

也许赋予神经网络无限可能性的“非线性”让神经网络模型走得太远，却也让它忘记了为什么出发（想想还挺哲学）。这也使得特征随着层层前向传播得到完整保留（什么也不做）的可能性都微乎其微。

用学术点的话说，这种神经网络丢失的“不忘初心”/“什么都不做”的品质叫做 **恒等映射（[identity mapping](https://www.zhihu.com/search?q=identity mapping&search_source=Entity&hybrid_search_source=Entity&hybrid_search_extra={"sourceType"%3A"answer"%2C"sourceId"%3A786270699})）**。

因此，可以认为 Residual Learning 的初衷，其实是让模型的内部结构至少有恒等映射的能力。以保证在堆叠网络的过程中，网络至少不会因为继续堆叠而产生退化！

### 二、**深度残差学习 Deep Residual Learning**

#### **1. 残差学习 Residual Learning**

前面分析得出，如果 <font color="#4d8bc6"> **深层网络** </font> 后面的层都是是 **恒等映射**，那么模型就可以转化为一个浅层网络。那现在的问题就是 **如何得到恒等映射** 了。

事实上，已有的神经网络很难拟合潜在的恒等映射函数 H(x) = x。

但如果把网络设计为 **H(x) = F(x) + x，即直接把恒等映射作为网络的一部分**。就可以把问题转化为 **学习一个残差函数 F(x) = H(x) - x.**

只要 F(x)= 0，就构成了一个恒等映射 H(x) = x。 而且，拟合残差至少比拟合恒等映射容易得多。

于是，就有了论文 [^3] 中的 Residual block 结构

<img src="https://pica.zhimg.com/80/v2-818b41c2f6a0e9345e382cb47ad54e08_720w.webp?source=1940ef5c" alt="img" style="zoom:50%;" />

Residual Block 的结构

图中右侧的曲线叫做跳接（shortcut connection），通过跳接在 **激活函数前，** 将上一层（或几层）**之前的输出与本层** 计算的 **输出相加**，将求和的结果输入到激活函数中做为本层的输出。

用数学语言描述，假设 Residual Block 的输入为 xxx ，则输出 yy y  等于：

<img src="https://picx.zhimg.com/80/v2-77589031a8e01bd900c02c9dff73ee98_720w.webp?source=1940ef5c" alt="img" style="zoom: 67%;" />

其中 F(x,{Wi})\mathcal{F}\left(x,\left\{W_{i}\right\}\right)\mathcal{F}\left(x,\left\{W_{i}\right\}\right) 是我们学习的目标，即输出输入的残差 y − xy-xy-x 。以上图为例，残差部分是中间有一个 Relu 激活的双层权重，即：

<img src="https://picx.zhimg.com/80/v2-c667773c43f2f51c0a096d74d454e2f4_720w.webp?source=1940ef5c" alt="img" style="zoom: 67%;" />

其中 σ\sigma \sigma  指代 Relu，而 W1, W2W_{1}, W_{2}W_{1}, W_{2} 指代两层权重。



*顺带一提，这里一个* *Block 中必须至少含有两个层* *，否则就会出现很滑稽的情况：*

<img src="https://pic1.zhimg.com/80/v2-83bfa1fb1caa188934e511a25c8ab074_720w.webp?source=1940ef5c" alt="img" style="zoom: 67%;" />

*显然这样加了和没加差不多……*

#### 2.**网络结构与维度问题**

<img src="https://pic1.zhimg.com/80/v2-03f393009c383ce8ec8b956399a105a8_720w.webp?source=1940ef5c" alt="img" style="zoom:50%;" />

ResNet 结构示意图（左到右分别是 VGG，没有残差的 PlainNet，有残差的 ResNet）

论文中原始的 ResNet34 与 VGG 的结构如上图所示，可以看到即使是当年号称“Very Deep”的 VGG，和最基础的 Resnet 在深度上相比都是个弟弟。

可能有好奇心宝宝发现了，跳接的曲线中大部分是实现，但也有少部分虚线。这些虚线的代表这些 Block 前后的维度不一致，因为去掉残差结构的 Plain 网络还是参照了 VGG 经典的设计思路：**每隔 x 层，空间上/2（下采样）但深度翻倍。**

也就是说，**维度不一致体现在两个层面**：

- **空间上** 不一致
- **深度上** 不一致

**空间上** 不一致很简单，只需要在跳接的部分给输入 x 加上一个线性映射 WsW_{s}W_{s} , 即：

<img src="https://picx.zhimg.com/80/v2-5f85db992a39b381c991073d85b9b829_720w.webp?source=1940ef5c" alt="img" style="zoom:67%;" />

而对于 **深度上** 的不一致，则有两种解决办法，一种是在跳接过程中加一个 1*1 的卷积层进行升维，另一种则是直接简单粗暴地补零。事实证明两种方法都行得通。

*注：深度上和空间上维度的不一致是分开处理的，但很多人将两者混为一谈（包括目前某乎一些高赞文章），这导致了一些人在模型的实现上感到困惑（比如当年的我）。*



### **三、Thinkings**

上述的内容是我以自己的角度思考作者提出 ResNet 的心路历程，我比作者蔡很多，所以难免出现思考不全的地方。

ResNet 是如此简洁高效，以至于模型提出后还有无数论文讨论“ResNet 到底解决了什么问题(The Shattered Gradients Problem: If resnets are the answer, then what is the question?)”[^4]

论文 [^4] 认为，即使 BN 过后梯度的模稳定在了正常范围内，但 **梯度的相关性实际上是随着层数增加持续衰减的**。而经过证明，ResNet 可以有效减少这种相关性的衰减。

对于 LLL 层的网络来说，没有残差表示的 Plain Net 梯度相关性的衰减在 12L\frac{1}{2^{L}}\frac{1}{2^{L}} ，而 ResNet 的衰减却只有 1L\frac{1}{\sqrt{L}}\frac{1}{\sqrt{L}} 。这也验证了 ResNet 论文本身的观点，网络训练难度随着层数增长的速度不是线性，而至少是多项式等级的增长（如果该论文属实，则可能是指数级增长的）



而对于“梯度弥散”观点来说，在输出引入一个输入 x 的恒等映射，则梯度也会对应地引入一个常数 1，这样的网络的确不容易出现梯度值异常，在某种意义上，起到了稳定梯度的作用。

除此之外，[shortcut](https://www.zhihu.com/search?q=shortcut&search_source=Entity&hybrid_search_source=Entity&hybrid_search_extra={"sourceType"%3A"answer"%2C"sourceId"%3A786270699}) 类似的方法也并不是第一次提出，之前就有“Highway Networks”。可以只管理解为，以往参数要得到梯度，需要快递员将梯度一层一层中转到参数手中（就像我取个快递，都显示要从“上海市”发往“闵行分拣中心”，[闵大荒](https://www.zhihu.com/search?q=闵大荒&search_source=Entity&hybrid_search_source=Entity&hybrid_search_extra={"sourceType"%3A"answer"%2C"sourceId"%3A786270699}) 日常被踢出上海籍）。而跳接实际上给梯度开了一条“高速公路”（取快递可以直接用无人机空投到我手里了），效率自然大幅提高，不过这只是个比较想当然的理由。

<img src="https://pic1.zhimg.com/80/v2-4047b234ff52295d0d6d1749ee931210_720w.webp?source=1940ef5c" alt="img" style="zoom: 80%;" />



上面的理解很多论文都讲过，但我个人最喜欢下面两个理解。

第一个已经由 Feature Pyramid Network [^5] 提出了，那就是跳连接相加可以实现不同分辨率特征的组合，因为浅层容易有高分辨率但是低级语义的特征，而深层的特征有高级语义，但分辨率就很低了。

第二个理解则是说，引入跳接实际上让模型自身 **有了更加“灵活”的结构**，即在训练过程本身，模型可以选择在每一个部分是“更多进行卷积与非线性变换”还是“更多倾向于什么都不做”，抑或是将两者结合。模型在训练便可以自适应本身的结构，这听起来是多么酷的一件事啊！

有的人也许会纳闷，我们已经知道一个模型的来龙去脉了，那么在一个客观上已经十分优秀的模型，强加那么多主观的个人判断有意思吗？

然而笔者还是相信，更多角度的思考有助于我们发现现有模型的不足，以及值得改进的点。比如我最喜欢的两个理解就可以引申出这样的问题“虽然跳接可以结合不同分辨率，但 ResNet 显然没有充分利用这个优点，因为每个 shortcut 顶多跨越一种分辨率（大部分还不会发生跨越）”。

那么“如果用跳接组合更多分辨率的特征，模型的效果会不会更好？”这就是 DenseNet 回答我们的问题了。

### **参考文献**

[^1]:https://www.coursera.org/learn/machine-learning
[^2]: Sandler M, Howard A, Zhu M, et al. MobileNetV2: Inverted Residuals and Linear Bottlenecks[J]. 2018.
[^3]:He K, Zhang X, Ren S, et al. Deep Residual Learning for Image Recognition[J]. 2015.
[^4]:Balduzzi D , Frean M , Leary L , et al. The Shattered Gradients Problem: If resnets are the answer, then what is the question?[J]. 2017.
[^5]:Lin T Y , Dollár, Piotr, Girshick R , et al. Feature Pyramid Networks for Object Detection[J]. 2016.



原文链接：Resnet 到底在解决一个什么问题呢？ - 薰风初入弦的回答 - 知乎 https://www.zhihu.com/question/64494691/answer/786270699

有用的专栏：[薰风的计算机科学家之路 - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/IsonomiaCS)

同济子豪兄（还有更多论文精读）：[ResNet 为什么能解决网络退化问题_哔哩哔哩_bilibili](https://www.bilibili.com/video/BV1vb4y1k7BV/?p=3&spm_id_from=pageDriver&vd_source=3659941460e6c74679750d458eaa5726)

batch Normalization 为什么能解决梯度消失？：[通俗易懂理解 Batch Normalization 和 Layer Normalization 归一化原理 - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/311165133)







## diffusion model 扩散模型

扩散模型这个概念其实在 2015 年就提出来了，只是在 22 年的时候，**哪篇工作** 彻底把扩散模型带火了。（在李沐读论文中有讲到，从 dell-e 到 dell-e 2 的发展历史 https://www.bilibili.com/video/BV17r4y1u77B/?spm_id_from

GAN 的优点：高保真（因为 GAN 本质是对抗的网络，着重优化的是保真度），但是多样性比 diffusion 差（在过程中没有随机性，多样性依赖于数据）

diffusion 的优点：由于是预测分布（VAE 的思想），在马尔科夫过程中引入了随机性，所以生成的多样性比 GAN 好。



### 扩散模型的发展之路

对于扩散模型的介绍：

随机在一张图片上一直加噪声，加的这个噪声我们知道，就是 gt

[吹爆！李宏毅教授半天就教会了我 Stable Diffusion 模型，原理详解+论文精读，深度解析生成式 AI 背后的原理！（人工智能/深度学习）_哔哩哔哩_bilibili](https://www.bilibili.com/video/BV1jV4y18713/?spm_id_from = 333.337.search-card.all.click&vd_source = 3659941460e6c74679750d458eaa5726)

最初版本的 diffusion 模型是怎么样的呢？他有什么缺点？DDPM 又如何优化了？



**小图主要提供语义信息，大图比小图多出来那部分增加的是感知信息。** [Latent Diffusion：开始的开始 - 知乎](https://zhuanlan.zhihu.com/p/652186695)



什么时候 diffusion 架构开始比 GAN 好了，用了什么技巧？（classifier guidance，classifier-free guidance）

google 的一篇论文，diffusion beat GAN







## DDPM 

![image-20241023094612782](../../AppData/Roaming/Typora/typora-user-images/image-20241023094612782.png)

贡献：

1. 只需要预测真实噪声和预测噪声之间的差值，有点 ResNet 的思想（以前都是直接预测这一步到下一步的噪声）
2. 预测噪声，就是预测一个正态分布（假设加的都是正态分布的噪声），预测分布就是预测均值和方差。DDPM 发现预测一个分布，甚至不用预测方差，将方差设置为一个常数，效果就已经很好了。

如今生成扩散模型的大火，则是始于 2020 年所提出的 [DDPM 论文](https://papers.cool/arxiv/2006.11239)（Denoising Diffusion Probabilistic Model），虽然也用了“扩散模型”这个名字，但事实上除了采样过程的形式有一定的相似之外，DDPM 与传统基于朗之万方程采样的扩散模型可以说完全不一样，这完全是一个新的起点、新的篇章。



## LDM

在 LDM 提出之前，diffusion model 的生成可控吗？

LDM ：就是让图片的特征在隐空间进行扩散，LDM 为何提出？

1. 已知，把图片压缩到隐空间再复原，是 VAE 的思想。

在隐空间扩散的效果和直接显示扩散的效果相比如何？



LDM 的贡献：

1-提出减少计算量，在隐空间进行加噪去噪的学习（相比于在像素层面进行加噪去噪，计算量少了很多）

2-提出了 cross attention？条件是 Q，K 还是 V，如果换一下会怎么样？



条件注入 stabel diffusion（是 LDM 的续作，stabel diffusion 并没有单独的论文，借鉴了谷歌的 Imagen）

为什么叫 stabel ，压缩到隐空间进行扩散为什么更加稳定，隐空间不是包含了更多的压缩信息，



## DALL-E 2





## VAE

[VAE 到底在做什么？VAE 原理讲解系列#1_哔哩哔哩_bilibili](https://www.bilibili.com/video/BV1sM4y1W7jx/?spm_id_from=333.337.search-card.all.click&vd_source=3659941460e6c74679750d458eaa5726)

[一个视频看懂 VAE 的原理以及关于 latent diffusion 的思考_哔哩哔哩_bilibili](https://www.bilibili.com/video/BV1wx421k74m/?spm_id_from=333.337.search-card.all.click&vd_source=3659941460e6c74679750d458eaa5726)

VAE 的目的就是构建一个平滑的概率分布，以便来生成图像（而不是按照训练时的离散样本来生成，这样在取到高维空间两个簇之间的特征向量来生成图像的时候，可能会生成噪声，）



VAE 就是一个类 Unet，Unet 就是最简单的编码器，瓶颈，解码器架构。



## VQ-VAE

[[1711.00937\] Neural Discrete Representation Learning](https://arxiv.org/abs/1711.00937)

引入了一个 codebook，来保存一些有代表性的向量，将 encode 出来的特征图中的每一个向量，与 codebook 中的向量求距离，用距离最近的 codebook 向量来“代表”特征图中的向量。

又把 VAE 所生成的连续的分布，变成离散的了，为什么？

并且这个 codebook 中的向量怎么初始化？（类似于聚类方法中，取样本点作为初始点？）















## 维度灾难

- “维数灾难”（Curse of Dimensionality）是在机器学习、数据挖掘和统计学等领域经常遇到的一个问题。它指的是随着数据维度（特征数量）的增加，数据分析和建模变得越来越困难的现象。例如，在一个二维空间（如平面直角坐标系）中，我们可以相对容易地对数据点进行可视化和分类。但当维度增加到高维空间（如 100 维）时，数据空间会变得极为复杂（因为很难找到足够近的邻居）。



问： 在图像中，encoder 最终会把图像压缩成一个高维向量，那我想知道，给定一个数据规模，我用多少维度的向量最合适，（就是不至于表征能力不够，但也不至于发生维度灾难）









## Delphi

论文地址：[[2406.01349\] Unleashing Generalization of End-to-End Autonomous Driving with Controllable Long Video Generation](https://arxiv.org/abs/2406.01349)

项目主页：[Unleashing Generalization of End-to-End Autonomous Driving with Controllable Long Video Generation](https://westlake-autolab.github.io/delphi.github.io/)

摘要：

使用生成模型合成新数据已成为自动驾驶解决数据稀缺问题的事实标准。尽管现有方法能够提升感知模型，但我们发现这些方法无法提高端到端自动驾驶模型的规划性能，因为生成的视频通常小于 8 帧，并且空间和时间的不一致不可忽略。为此，我们提出了 *Delphi*，一种新颖的基于扩散的长视频生成方法，具有 **跨多视图的共享噪声建模机制**，以提高空间一致性，以及一个 **特征对齐模块**，以实现精确可控性和时间一致性。我们的方法可以生成多达 40 帧的视频而不会失去一致性，与最先进的方法相比，这大约是 5 倍。我们不是随机生成新数据，而是进一步 **设计了一个抽样策略，让 *Delphi* 生成与那些失败情况类似的新数据，以提高抽样效率**。这是通过在预先训练的视觉语言模型的帮助下构建失败案例驱动的框架来实现的。我们广泛的实验表明，我们的 *Delphi* 生成的长视频质量超过了以前最先进的方法。因此，仅生成 4% 的训练数据集大小，我们的框架就能够超越感知和预测任务，据我们所知，首次将端到端自动驾驶模型的规划性能提高了 25%。

<img src="../../AppData/Roaming/Typora/typora-user-images/image-20241028201712319.png" alt="image-20241028201712319" style="zoom:80%;" />

#### 1. 跨多视图的共享噪声

- 发现问题：过短的视频生成，对 end-to-end 的提升不大，之前方法只能在保持空间和时间一致性的前提下生成 8 帧，而 Delphi 可以生成 40 帧。

![MY ALT TEXT](https://westlake-autolab.github.io/delphi.github.io/static/images/delphi-framework-small.png)

m：一个应用于一个 camera view 的所有帧的噪声，不变。

p：应用于同一帧的所有视图，随着帧数 n 的改变而改变。

<img src="../../AppData/Roaming/Typora/typora-user-images/image-20241028195349360.png" alt="image-20241028195349360" style="zoom: 67%;" />



#### 2. 特征对齐

- 发现问题：之前的方法只是简单的对 previous frames 做 cross attention ，并没有考虑到位于不同网络深度的特征的感受野不一样。导致空间和时间的一致性不好。

<img src="../../AppData/Roaming/Typora/typora-user-images/image-20241028202406809.png" alt="image-20241028202406809" style="zoom:67%;" />

<img src="../../AppData/Roaming/Typora/typora-user-images/image-20241028203530481.png" alt="image-20241028203530481" style="zoom:67%;" />



#### 3. 针对失败案例的抽样策略

- 发现问题：以前的方法都是从数据集里面随机抽样，但是数据是长尾分布的，对于 corner case （那个尾巴）的针对性优化非常重要，并且针对端到端模型做得不好的 case 来优化，才能减少计算成本。

![MY ALT TEXT](https://westlake-autolab.github.io/delphi.github.io/static/images/failure-case-driven%20framwork.jpeg)

#### 限制、缺点：

1. 只能改变外观，不能改变布局 layout
2. 当 end-to-end model 在训练集上表现很好的时候，失败案例抽样策略失效。





## SimGen（NeurlPS 2024）

论文地址：[arxiv.org/pdf/2406.09386](https://arxiv.org/pdf/2406.09386)

项目地址：[GitHub - metadriverse/SimGen: Simulator-conditioned Driving Scene Generation](https://github.com/metadriverse/SimGen)

摘要：

可控的合成数据生成可以大大降低自动驾驶研发中训练数据的标注成本。以前的作品使用扩散模型来生成以 3D 对象布局为条件的驾驶图像。但是，这些模型是在 nuScenes 等小规模数据集上训练的，这些数据集缺乏外观和布局多样性。此外，经过训练的模型只能根据来自同一数据集验证集的真实布局数据生成图像，其中可能会发生过拟合。在这项工作中，我们介绍了一个名为 SimGen 的模拟器条件场景生成框架，该框架可以通过 **混合来自模拟器和现实世界的数据来学习** 生成多样化的驾驶场景。它使用一种新颖的 **级联扩散管道** 来解决具有挑战性的 **模拟到真实差距** 和 **多条件冲突**。**收集驾驶视频数据集 DIVA** 是为了增强 SimGen 的生成多样性，其中包含来自全球 73 个地点的超过 147.5 小时的真实驾驶视频和来自 MetaDrive 模拟器的模拟驾驶数据。SimGen 实现了卓越的生成质量和多样性，同时保留了基于文本提示和从仿真器中提取的布局的可控性。我们进一步展示了 SimGen 为 BEV 检测和分割任务的合成数据增强带来的改进，并展示了其在安全关键数据生成方面的能力。将提供代码、数据和模型。

<img src="../../AppData/Roaming/Typora/typora-user-images/image-20241028204959818.png" alt="image-20241028204959818" style="zoom:80%;" />



#### 1. 数据集 DIVA

发现问题：现有的模型，第一，因为只使用了 nusence 这种相对比较小的数据集，导致背景和车的外观比较单一。第二，只能改变外观，不能改变布局。
 method：
 针对第一点，收集了一个数据集。
 分为两个部分：

- 一部分是 DiVA-real，这部分是从 YouTube 上收集的各种驾驶视屏，包含了非常多样的道路布局，天气，交通元素， 环境等。（解决 appearance diversity 的问题）
-  另一部分是 DIVA-sim，这部分是由模拟器生成的，模拟器用的是 Metadrive，理论上提供地图信息，模拟器就可以根据预先定义的规则和交互式的策略，来生成任何驾驶场景的数字孪生。 模拟器根据真实世界的数据，生成数字孪生，用来 train Cond diff，用于弥补模拟数据和真实世界数据的细节上的差异。然后还可以生成真实世界没有的 layout，还有一些危险驾驶的数据案例。
- <img src="../../AppData/Roaming/Typora/typora-user-images/image-20241028205129605.png" alt="image-20241028205129605" style="zoom: 67%;" />

<img src="../../AppData/Roaming/Typora/typora-user-images/image-20241028205042948.png" alt="image-20241028205042948" style="zoom:67%;" />

#### 2. 级联扩散 pipeline

<img src="../../AppData/Roaming/Typora/typora-user-images/image-20241028205235409.png" alt="image-20241028205235409" style="zoom: 80%;" />





#### 思考：

 其实 SimGen 也还没有做到真正的闭环，目前的模型貌似也还远没有做到，都是增强训练集。

 如果说，可以把 SimGen 做到视屏生成四十多帧的话，就相当于打破了 layout 的这个限制，模型可以在虚拟世界里面不断的自我迭代（离线训练），并且可以一直不断的去训练那些关键安全驾驶场景。这样就完全弥补了数据上的缺陷。
