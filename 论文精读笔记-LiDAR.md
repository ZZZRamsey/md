## LiDMs（CVPR 2024）

论文地址：[2404.00815\] Towards Realistic Scene Generation with LiDAR Diffusion Models](https://arxiv.org/abs/2404.00815)

项目地址：[GitHub - hancyran/LiDAR-Diffusion: CVPR 2024 Official implementation of "Towards Realistic Scene Generation with LiDAR Diffusion Models"](https://github.com/hancyran/LiDAR-Diffusion)

摘要：

扩散模型 （DM） 在照片级真实感图像合成方面表现出色，但它们对 LiDAR 场景生成的适应构成了很大的障碍。这主要是因为在点空间中运行的 DM 难以保留 LiDAR 场景的曲线状图案和 3D 几何图形，这消耗了它们的大部分表示能力。在本文中，我们提出了 LiDAR 扩散模型 （LiDMs），通过 **将几何先验纳入学习管道**，从潜在空间生成 LiDAR 逼真的场景，以捕捉 LiDAR 场景的真实感。我们的方法针对三个主要领域：模式真实感、几何真实感和对象真实感。具体来说，我们 **引入了曲线压缩（Curve-wise Encoding）** 来模拟真实世界的 LiDAR 模式，**引入逐点坐标监督** 来学习场景几何图形，以及 **用于完整 3D 对象上下文的区块编码（patch-wise Encoding）**。凭借这三个核心设计，我们的方法在 64 光束场景中实现了无条件 LiDAR 生成方面的竞争性能，并在条件 LiDAR 生成方面取得了最先进的技术，同时与基于点的 DM 相比保持了高效率（速度提高了 107 倍）。此外，通过将 LiDAR 场景压缩到潜在空间，我们实现了具有语义图、相机视图和文本提示等各种条件的 DM 的可控性。

<img src="https://github.com/hancyran/LiDAR-Diffusion/blob/main/assets/overview.png?raw=true" alt="overview.png" style="zoom: 23%;" />

#### 1. Curve-wise 和 patch-wise Encoding

- 发现问题：

  之前的方法没有关注到点云数据中的 曲线状结构，曲线状结构 是指一段密集连续的点。这一点在[2303.12050\] CurveCloudNet: Processing Point Clouds with 1D Structure](https://arxiv.org/abs/2303.12050)已经提出过。

  patch-wise 其实就是在latent space（感受野比较大）进行下采样，

  <img src="../../AppData/Roaming/Typora/typora-user-images/image-20241031211713558.png" alt="image-20241031211713558" style="zoom: 150%;" />

- 解决问题：引入Curve-wise Encoding ，在Curve-wise block中，卷积核大小为1x4，并且每个上采样和下采样层仅在水平方向上应用。



#### 2. 逐点坐标监督（损失函数）

<img src="../../AppData/Roaming/Typora/typora-user-images/image-20241031215743211.png" alt="image-20241031215743211" style="zoom:67%;" />

使用L_VQ来学习codebook
