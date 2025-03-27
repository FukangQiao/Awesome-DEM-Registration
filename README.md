# Awesome-DEM-Registration
[**Image registration**](https://en.wikipedia.org/wiki/Image_registration) is the process of transforming different sets of data into one coordinate system. Data may be multiple photographs, and from different sensors, times, depths, or viewpoints.

It is used in computer vision, medical imaging, military automatic target recognition, compiling and analyzing images and data from satellites. Registration is necessary in order to be able to compare or integrate the data obtained from different measurements. 



**[Learning Resources](#Learning-Resources)**

- [Paper] (## DEM-Registration paper)
- [Repository](## DEM-Registration repository)

## DEM-Registration paper

COSSI-CORR

**- Image Registration Review**
Zitová, B., & Flusser, J. (2003). "Image registration methods: a survey."
这篇综述系统性地总结了图像配准的基本框架（特征提取、特征匹配、变换模型、重采样）以及传统算法（基于灰度、特征、频域的方法）。
Ma, J., et al. (2021). "Image matching from handcrafted to deep features: A survey."
涵盖从SIFT、SURF到深度学习（如SuperPoint、LoFTR）的特征匹配方法演进，适合了解技术发展脉络。

**- DEM-Registration**


## DEM-Registration repository

- [DORIS]()  doris_core/coregistration.cc
- DEM-coreg


## References

[1]Altena, B., & Nattino, F. dhdt: A photohypsometric Python library to estimate glacier elevation change via optical remote sensing imagery (Version 0.1.0) [Computer software]. https://github.com/GO-Eratosthenes/dhdt

### Advice
（1）数据预处理是关键

去噪与平滑：DEM常包含噪声（如传感器误差），使用高斯滤波或形态学操作预处理。
空洞填补：缺失区域（如云覆盖）需插值修复，避免配准偏差。

（2）特征选择需因地制宜
传统图像特征（如SIFT）在平坦地形中可能失效，需结合地形特征（如河流交汇点、山顶点）。
对多源DEM（如SRTM与LiDAR），优先使用高程梯度、曲率等几何特征。

（3）多尺度策略提升鲁棒性
先通过低分辨率DEM完成粗配准，再逐步细化到高分辨率数据。

（4）评估指标需多样化
定量指标：RMSE（均方根误差）、地形一致性（如坡度/坡向差异）。
定性验证：叠加等高线或山体阴影图进行人工检查。

（5）混合方法优于单一方法
例如：先用ICP进行粗配准，再用互信息优化局部对齐；或结合深度学习与传统特征。

（6）公开数据集与工具
数据集：NASADEM、ASTER GDEM、ICESat-2 ATL06高程点。
工具：PDAL（点云处理）、GDAL（DEM读写）、Elastix（医学配准工具改造）。

（7）关注地形变化与时间效应
多时相DEM配准需考虑地形变化（如冰川退缩、滑坡），必要时引入形变模型。

总结：
DEM配准的核心挑战在于**处理多源数据的分辨率差异、地形特征稀疏性以及噪声干扰**。建议从经典算法（如ICP+特征匹配）入手，逐步结合深度学习（如3D CNN）和领域知识（地形地貌学）。可优先复现近年顶会论文（如IGARSS、CVPR）中的DEM配准实验，再针对具体场景改进。