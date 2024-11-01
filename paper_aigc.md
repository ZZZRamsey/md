[TOC]

- **Tag**（发表时间，被什么会议/期刊接受，论文地址，代码是否开源，仓库地址，是否已复现）

会议/期刊：

论文地址：

代码地址：

- **Baseline**（如果有，对比了之前的什么方法）

- **Architecture**（论文中的模块结构图，公式表达）

- **Method**（最主要的，总结作者的思考过程，1-发现了什么问题，2-如何针对设计的解决方案，3-解决方案为何 work）
- **Ablation Study**（消融实验）
- **Limitation Analysis**（问题分析）
- **Note**（自由发挥区，可以写点自己的想法）
  - **Future Work**（可能的改进方案）
  - **Blog**（可以补充一些较好的博客）

---



# STREET VIEW GENERATION WITH DIVERSE 3D GEOMETRY CONTROL

## 分类

### MagicDrive: Street View Generation with Diverse 3D Geometry Control	多种 3D 几何控制的街景生成

- **Tag**

会议/期刊：ICLR 2024

论文地址： http://arxiv.org/abs/2310.02601

代码地址：[cure-lab/MagicDrive: ICLR24 Official implementation of the paper “MagicDrive: Street View Generation with Diverse 3D Geometry Control” (github.com)](https://github.com/cure-lab/MagicDrive?tab=readme-ov-file)

- **Baseline**

BEVGen，BEVControl

- **Architecture**

![image-20231011165634648](https://github.com/cure-lab/MagicDrive/raw/main/assets/overview.png)

- **Method**


1. 对不同控制信息使用不同的 encode 方法
   - 文本使用 Clip

   - 相机和 bbox 的框有一个共同点，都是 **离散** 的，本文对这种标注，使用 **傅里叶嵌入（Fourier embedding）** 后，再过一个 MLP。
   - bbox 的类名使用 Clip 转为向量之后，使用了一次均值池化（为什么要均值池化？有论文论证 4.1）
   - 地图属于网格数据，文中讨论了以前将 BEV 转化为 FPV（First-Person-View）的方法，该方法会造成信息损失。文中提出使用额外的一个 encoder 进行嵌入，并与相机的 embed 和 相机 的 embed 进行融合（bbox 的 embed 可以提供路面高度信息，相机内外参告诉模型，需要使用Road map 的哪一块）

2. 交叉注意力模块

   - 问题：在 BEV 视图时，相邻视图的边缘位置，可能出现视图不匹配。


   - 本文提出使用交叉注意力从左右视图获取语义信息，以增强生成的一致性。用当前视图作 Q，左右视图作 K，V。对视频帧使用，也保证了视频生成的一致性。


![image-20241010115134450](https://raw.githubusercontent.com/ZZZRamsey/PicGo_save/main/202410102259670.png)

3. 训练 trick - 4.3 小节	

   - 对bbox进行过滤，只留相机看得见的框（也可能是有障碍物遮挡，需要过滤），减少bbox encoder的压力，也就减少了GPU资源的消耗。并随机添加一些不可见的 box，增强模的几何迁移的能力（为什么？）

   - 在训练过程中随机丢弃条件 Classifier-free Guidance（有论文论证 4.3）



- **Ablation Study**

本任务的评价指标包含 FID（Frechet Inception Distence 生成质量的指标） 和对下游任务指标的提升（检测-mAP、NDS，分割-Road mIOU、Vehicle mIOU）

为解决下游任务的输入分辨率的不匹配问题，本文使用了两种不同倍率的下采样（可进行设置）。

使用了两种方式测试生成效果：

一、使用 val 的标注生成，给使用 train 训练好的 CVT 和 BEVFusion 检测和分割，算指标。对比使用原 val 推理的。

二、使用 train 的标注生成，并用生成的来训练CVT 和 BEVFusion，然后使用训好的，对原 val 进行推理，算指标。对比使用原 train 训练的。

- **Limitation Analysis**

noseen视角的生成泛化性不强，对于夜晚场景的生成真实度不好，尚未支持更多自然语言的描述，前置生成

- **Note**
  - **Future Work**

    Fourier embedding 是一种处理离散数据比较有优势的方法？是否可以用到点云的处理中 ？

    更多数据源的输入，使用 LiDAR，其实就是 ViDAR 反过来

    <img src="https://raw.githubusercontent.com/ZZZRamsey/PicGo_save/main/202410102259672.png" alt="image-20241010221241796" style="zoom: 50%;" />

  - **Blog**

    [ICLR24 | MagicDrive - 基于 3D 几何条件控制的自动驾驶街景数据生成_哔哩哔哩_bilibili](https://www.bilibili.com/video/BV1EC4y167BR/?spm_id_from=333.337.search-card.all.click&vd_source=3659941460e6c74679750d458eaa5726)



# POINT CLOUD GENERATION WITH DIVERSE 3D GEOMETRY CONTROL

## 分类

### 论文标题+中文翻译

- **Tag**

会议/期刊：

论文地址：

代码地址：未开源/计划开源/仓库地址

- **Baseline**

- **Architecture**
- **Method**
- **Ablation Study**
- **Limitation Analysis**
- **Note**
  - **Future Work**
  - **Blog**