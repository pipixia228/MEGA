链接：
	* parper：[]()https://arxiv.org/abs/2212.10156
	* code:[]()https://github.com/OpenDriveLab/UniAD
# 核心点
1. 以规划为导向的端到端
2. 提升了可解释性
# 框架
![[UniAD框架.png]]
**UniAD最终包括四个基于Transformer解码器的感知和预测模块以及一个规划器**
1. Backbone：图像信息特征提取（eg：BEV Former）
2. Perception（感知）: Tracking Former and Mapping Former
	1. Tracking Former：与背景车交互
	2. Mapping Former：与地图角互
	3. 将背景车交互结果、地图交互结果、BEV Feature都给到下一模块（Prediction）
3. Prediction（预测）：
	1. Motion Former：以场景为中心的方式预测所有代理的多模式未来运动
	2. Occ Former:
		1. 密集场景特征在展开到未来视野时通过精心设计的注意力模块获取代理级特征==(背景车行为)==
		2. 过代理级特征和密集场景特征之间的矩阵乘法轻松产生实例占用率==（计算栅格占用）==
4. Plannin（规划）
5. Learning（训练）：两个阶段
	1. 联合训练几个epoch(实验中为6个)的感知部分，即跟踪和映射模块
	2. 用所有的感知、预测和规划模块端到端训练20个epoch的模型