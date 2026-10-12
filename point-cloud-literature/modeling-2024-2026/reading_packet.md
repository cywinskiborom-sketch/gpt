# 点云建模典型论文：2024–2026 六刊摘要中译与流程导读

这份材料用于第一轮“多、广、浅”的阅读。选取12篇输入输出清楚、方法有对照意义的论文，帮助理解点云如何变成表面、网格、结构模型与BIM。“典型”指适合学习流程与问题，不是经全刊计量统计得到的热度或引用排名。

## 阅读范围与来源

本册主要收录“点云输入→模型输出”的研究，也明确标出影像/SfM上游与树冠条件生成的差别。重建已有观测几何、生成合理的缺失结构、恢复纹理、生成工程构件，是相关但不同的目标。

年份覆盖2024–2026。11篇有该范围内的期刊卷期，AUPOME为2026-08-16在线优先预出版，正式卷期未核实，单列状态。DOI中的年份不等于卷期年，例如I-Filtering为2026卷期、2025首次在线。检索核验截至2026-10-12。

7篇为完整摘要中译：4篇来自你上传的IEEE题录，3篇原文明确为CC BY开放许可。5篇为中文摘要要点，原摘要链接均给出；这些是自行归纳，不能当作逐句译文。全文实验只核对了文中明确列出的表格或节选，未声称精读所有论文。过程说明与阅读建议是导读，不属于原摘要。

## 怎么读：先四篇，再按问题扩展

先读10 Cloud2BIM、03 BSS、01 RR-Net、09 I-Filtering，分别理解工程规则、结构优化、学习＋几何和隐式建模。每篇第一遍可用约10–15分钟：摘要→总流程图→一项实验→一项限制。无需马上读完数学推导。

再读04 Point2Building与02 SCGNet，比较怎样从点云直接生成顶点和面。外观建模看05 ColorMesh，树结构生成看06；工程知识看11，快速采集规划看08，少标签工程建模看12，最新联合上采样/网格流程看07。第一轮约2–3小时，可分几次完成。

## 一条可复用的流程认识

原始点云与可用影像/位姿→检查噪声、密度、遮挡与配准→构造邻域几何、结构特征或学习特征→选择表面/结构表示→生成网格或参数模型→同时检查几何、拓扑、外观与效率。

不同方法会合并或替换步骤。例如学习式模型可能直接预测顶点和面；隐式方法先得到连续场，再提取表面；BIM还要定义有厚度、有类别和关系的工程构件。分割通常只是其中一步，逐点类别不是最终几何模型。

## 读效果时的四个检查

- 看评价对象：边缘检测、线框、完整网格、纹理和BIM是不同输出，指标不能相互替代。
- 看单位与口径：CD可能归一化或采用不同定义；“0.021”没有单位时不能转换成厘米。
- 看条件：训练/测试城市、重新训练与零样本迁移、是否提供实例/法向、采样与阈值均会影响结果。
- 看计时范围：单个模块、代理模型、完整IFC导出和包含SfM的整条流程，耗时不能直接混比。

文中数值仅说明各论文自己的实验，不能据此给12篇排总榜。



## 论文索引


| 编号 | 论文入口 | 期刊 | 年份 |
|---|---|---|---|
| 01 | RR-Net：屋顶线框 | TGRS | 2025 |
| 02 | SCGNet：上下文引导建筑生成 | TGRS | 2026 |
| 03 | BSS：结构骨架与优化 | ISPRS JPRS | 2024 |
| 04 | Point2Building：自回归建筑网格 | ISPRS JPRS | 2024 |
| 05 | ColorMesh：几何与纹理 | JAG | 2024 |
| 06 | 树冠到树模型：图网络与最小生成树 | JAG | 2024 |
| 07 | AUPOME：上采样与网格提取 | Pattern Recognition | 2026 在线优先 |
| 08 | 城市建筑轻量代理模型 | TPAMI | 2024 |
| 09 | I-Filtering：保细节隐式距离场 | TPAMI | 2026 |
| 10 | Cloud2BIM：点云到IFC | Automation in Construction | 2025 |
| 11 | 工程知识与参数化体积模型 | Automation in Construction | 2024 |
| 12 | 少标签高架桥BIM | Automation in Construction | 2026 |


## 01 RR-Net：屋顶线框

RR-Net: 3-D Roof Reconstruction From Airborne LiDAR Point Clouds via Edge Segmentation and Wireframe Generation

RR-Net：通过边缘分割与线框生成，从机载 LiDAR 点云重建三维屋顶

作者：Yike Xu；Li Cao；Shengling Geng；Xiaoping Liu

出处：IEEE Transactions on Geoscience and Remote Sensing，2025，63，1–13。

期刊卷期年：2025；首次在线：27 Oct 2025。

DOI：https://doi.org/10.1109/TGRS.2025.3625669

### 摘要

完整摘要中译，原文来自用户上传IEEE题录。

从机载激光雷达（LiDAR）点云重建三维屋顶，是遥感与摄影测量领域的一项重要任务。由于 LiDAR 点云本身具有噪声较大、数据量庞大和结构复杂等特点，传统点云处理方法在精度和鲁棒性方面的表现有限。多数现有方法依靠角点检测和边缘预测来提取并重建屋顶结构。然而，角点通常分布稀疏，难以准确定位，从而导致明显的几何偏差和不完整的结构重建。因此，从复杂的 LiDAR 点云生成高质量三维屋顶，仍是一个有待解决的挑战。为解决这些问题，我们提出了一种结合边缘分割与线框生成的新型屋顶重建方法 RR-Net。首先，我们开发了一种创新的统一点云边缘分割网络，将边缘检测、分割和去噪整合在一起。其次，基于该网络的分割结果，我们设计了一套高效、鲁棒的线框生成与屋顶重建流程，实现从机载 LiDAR 点云到屋顶模型的自动转换。在 Building 数据集上的大量实验表明，RR-Net 能够高效、准确地从机载 LiDAR 点云重建屋顶。RR-Net 的边缘检测准确率达到 95.7%，并将线框的 Chamfer 距离（CD）误差降至 0.021。RR-Net 的结果已公开于：https://yecoxu.github.io/publications/RR-Net/ 。

### 流程、方法和效果

输入输出：输入：机载 LiDAR 建筑/屋顶点云；输出：屋顶线框以及由线框重建的三维屋顶模型。摘要没有明确说明是否同时负责从整座城市点云中提取建筑。

流程：机载 LiDAR 屋顶点云进入统一边缘分割网络。 → 网络联合执行边缘检测、边缘分割和去噪，获得结构边缘信息。 → 根据分割结果生成屋顶线框。 → 以线框为结构骨架重建三维屋顶模型。

方法：以边缘为中间表示，统一边缘检测、分割与去噪，再把学习得到的结构信息交给几何重建流程；避免将角点定位当作唯一入口。

效果与条件：作者在 Building 数据集上报告边缘检测准确率 95.7%、线框 CD 误差 0.021。这两个数分别评估边缘预测与线框几何，不能直接当作整个屋顶模型的统一质量分数。

限制：摘要未报告运行时间、与具体基线的数值差距、跨城市泛化实验或闭合/拓扑正确率；这些需要查看正文实验设置。

粗读重点：优先看总流程图，辨认“原始点云→边缘分割→线框→屋顶面”的中间结果；再看线框连通规则、消融实验，以及 CD 的计算设置。

证据范围：效果主要依据摘要；未补造缺失数字。

来源核验：https://yecoxu.github.io/


## 02 SCGNet：上下文引导建筑生成

Integrating Spatial Context With Generative Model for Building Reconstruction From Airborne LiDAR Point Clouds

融合空间上下文与生成模型，从机载 LiDAR 点云重建建筑

作者：Yuxiang Zhao；Shengwen Li；Fang Fang；Nan Min；Sishi Gong；Yu Wang；Shunping Zhou

出处：IEEE Transactions on Geoscience and Remote Sensing，2026，64，1–13。

期刊卷期年：2026；首次在线：3 Mar 2026。

DOI：https://doi.org/10.1109/TGRS.2026.3670027

### 摘要

完整摘要中译，原文来自用户上传IEEE题录。

从机载激光雷达（LiDAR）点云（PCs）重建三维建筑，是一项基础任务，对城市规划、自动驾驶和应急服务等应用具有重要意义。新兴的生成模型方法在这项任务中取得了显著进展。然而，以往方法未能充分利用点云本身包含的空间上下文，导致建筑重建不准确。本研究提出了一种名为 SCGNet 的新方法，将空间上下文与生成模型融合，以提高三维建筑模型的重建质量。具体而言，首先引入基于全局上下文的顶点生成（GCVG）模块，预测建筑顶点。随后，开发以顶点为中心的多尺度空间上下文编码（VMSCE）模块，捕获以建筑顶点为中心的空间上下文的多尺度语义信息。最后，设计局部上下文增强的面生成（LCFG）模块，重建建筑面。大量实验表明，所提出的方法优于基线方法，并具有鲁棒性。本研究探索了一条优化建筑重建的新途径，并为基于点云的三维模型任务提供方法参考。源代码、模型权重和数据集将公开于：https://github.com/ShuaibZyx/SCGNet 。

### 流程、方法和效果

输入输出：输入：机载 LiDAR 建筑点云；输出：由生成的建筑顶点和面构成的三维建筑模型/网格。

流程：从机载 LiDAR 点云获取建筑的全局空间上下文。 → GCVG 模块借助全局上下文预测建筑顶点。 → VMSCE 模块围绕顶点编码多尺度空间上下文与语义信息。 → LCFG 模块利用局部上下文生成建筑面，形成三维建筑模型。

方法：将三维模型生成分成顶点预测、顶点中心的多尺度上下文编码和面生成三部分，使生成器直接利用点云中的结构约束。这里“生成模型”并不自动等同于扩散模型，摘要未明确具体生成架构。

效果与条件：摘要只报告作者结论：优于基线且具有鲁棒性，没有给出具体数值、基线名称或鲁棒性测试条件。作者仓库提供 Zurich、Tallinn、AHN3 数据入口，具体定量比较应查论文实验表。

限制：不能仅据摘要断言达到全领域最优、提高多少个百分点或对任意城市均能泛化；需要正文中的重建误差、覆盖率、模型复杂度和失败案例。

粗读重点：看总流程图中的顶点与面是否分别生成；找 GCVG/VMSCE/LCFG 的消融表，判断“全局信息”和“局部信息”分别减少了什么错误；注意训练城市与测试城市的划分。

证据范围：效果主要依据摘要；未补造缺失数字。

来源核验：https://github.com/ShuaibZyx/SCGNet


## 03 BSS：结构骨架与优化

A novel Building Section Skeleton for compact 3D reconstruction from point clouds: A study of high-density urban scenes

面向点云紧凑三维重建的新型建筑截面骨架：高密度城市场景研究

作者：Yijie Wu；Fan Xue；Maosu Li；Sou-Han Chen

出处：ISPRS Journal of Photogrammetry and Remote Sensing，2024，209，85–100。

期刊卷期年：2024；首次在线：未核实具体日期。

DOI：https://doi.org/10.1016/j.isprsjprs.2024.01.020

### 摘要

中文摘要要点（自行归纳），不冒充原文逐句译文。

作者利用建筑的平行、对称关系，将带法向的点云组织成截面骨架，再提出候选体块。通过整数规划权衡拟合误差与模型复杂度，合并体块并生成紧凑网格。在15个场景、60余栋建筑上的比较，同时评价几何误差、模型简洁性与效率。

### 流程、方法和效果

输入输出：城市建筑点云→紧凑多边形网格。

流程：点云→截面骨架→候选体块→整数规划→网格

方法：建筑结构先验＋离散优化。

效果与条件：平均每场景623个三角形、RMSD 0.82 m、110 s；摘要未列计时硬件。

限制：单主方向及平行/对称假设限制复杂曲面，缺失处可能出现缝隙。

粗读重点：看图3、§4.1的候选生成，及§6.2失败情况。

证据范围：效果主要依据摘要；未补造缺失数字。

来源核验：https://hub.hku.hk/handle/10722/340070；https://frankxue.com/pdf/wu24bss.pdf


## 04 Point2Building：自回归建筑网格

Point2Building: Reconstructing buildings from airborne LiDAR point clouds

Point2Building：从机载 LiDAR 点云重建建筑

作者：Yujia Liu；Anton Obukhov；Jan Dirk Wegner；Konrad Schindler

出处：ISPRS Journal of Photogrammetry and Remote Sensing，2024，215，351–368。

期刊卷期年：2024；首次在线：2024-07-26。

DOI：https://doi.org/10.1016/j.isprsjprs.2024.07.012

### 摘要

完整摘要中译，原文开放许可；见文末来源与许可。

我们提出一种基于学习的方法，将机载 LiDAR 点云中的建筑重建为三维多边形网格。从机载 LiDAR 数据重建三维建筑的困难在于：建筑设计、尤其是屋顶形状具有很大的多样性；场景中的点密度较低且变化明显；此外，植被遮挡或传感器观测角度往往导致建筑立面的覆盖不完整。为应对形状多样性以及不均匀、不完整的物体覆盖，我们引入一个生成模型，直接根据输入点云预测三维多边形网格。这个名为 Point2Building 的自回归模型，通过生成顶点序列和面序列，逐步构建网格。这种方式使模型能够灵活适应不同的几何形状和建筑结构。许多现有方法高度依赖穷尽式平面检测等预处理步骤，而我们的模型直接从点云数据中学习，从而减少误差传递，并提高重建的保真度。我们在来自苏黎世、柏林和塔林的一组机载 LiDAR 数据上进行了实验验证。我们的方法对不同的城市风格表现出良好的泛化能力。

### 流程、方法和效果

输入输出：输入：已分到单栋建筑的机载 LiDAR 点云；输出：建筑外表面的多边形网格（顶点与面），不是语义标签。

流程：借助类别标签与参考轮廓得到单栋建筑点云，并归一化 → 用稀疏三维卷积编码点云特征 → 自回归 Transformer 逐个生成顶点坐标 → 面模块逐个生成连接顶点的多边形面 → 检查几何合理性，拒绝不合理生成结果并重新采样

方法：SparseCNN 编码＋两个自回归模块分别生成顶点与面，借鉴 PolyGen；用合理性规则与拒绝采样控制生成失误。

效果与条件：摘要只给跨城市效果的定性判断。正文表 2（苏黎世对照实验）报告平均距离误差 MDE 0.2542 米，City3D 为 0.3046 米；Chamfer 距离 0.3060 米，City3D 为 0.3708 米。正文第 4.7 节明确在柏林、塔林分别重新训练，不能把摘要的泛化表述理解为跨城零样本直接迁移。

限制：需要已分离单栋建筑点云和网格监督；复杂屋顶与微小构件仍较困难；不显式保证水密性/流形性；顶点与面分开预测；各城结果包含重新训练，不是零样本跨城证明。

粗读重点：重点看图 1 的顶点→面流程、图 2 的点云编码器、表 2 的距离指标、图 16 的失败案例；认真读第 4.7–4.8 节，区分生成合理性、水密性与跨域泛化。

证据范围：已核对正文指定实验表/节选。

来源核验：https://arxiv.org/pdf/2403.02136v2；https://www.sciencedirect.com/science/article/pii/S092427162400279X


## 05 ColorMesh：几何与纹理

ColorMesh: Surface and texture reconstruction of large-scale scenes from unstructured colorful point clouds with adaptive automatic viewpoint selection

ColorMesh：通过自适应自动视点选择，从无结构彩色点云重建大规模场景的表面与纹理

作者：Mubai Li；Zhenxin Zhang；Siyun Chen；Liqiang Zhang；Zhihua Xu；Xiaoxu Ren；Jinlan Liu；Peng Sun

出处：International Journal of Applied Earth Observation and Geoinformation，2024，132，104041。

期刊卷期年：2024；首次在线：未核实具体日期。

DOI：https://doi.org/10.1016/j.jag.2024.104041

### 摘要

中文摘要要点（自行归纳），不冒充原文逐句译文。

ColorMesh将无结构彩色点云转换为带纹理网格。它先自动选择虚拟视点，将点云投影为多幅图像；利用可见性网络与图割恢复表面，再由纹理网络修补稀疏颜色并完成贴图。学习模块负责预测，几何求解负责组成模型，是几何与外观联合建模的实例。

### 流程、方法和效果

输入输出：RGB点云（无需法向）→网格＋纹理。

流程：虚拟视图→VisNet→图割网格→TexNet→贴图

方法：可见性学习＋几何优化＋纹理修补。

效果与条件：摘要未给精度或耗时数字；效果仅能作定性理解。

限制：本文未核对实验表，几何精度与外观质量须分开检查。

粗读重点：读图2，追踪两个网络如何服务于网格与纹理。

证据范围：效果主要依据摘要；未补造缺失数字。

来源核验：https://www.sciencedirect.com/science/article/pii/S1569843224003959；https://doi.org/10.1016/j.jag.2024.104041


## 06 树冠到树模型：图网络与最小生成树

Accelerated forest modeling from tree canopy point clouds via deep learning

利用深度学习，从树冠点云快速构建森林模型

作者：Jiabo Xu；Zhili Zhang；Xiangyun Hu；Tao Ke

出处：International Journal of Applied Earth Observation and Geoinformation，2024，132，104074。

期刊卷期年：2024；首次在线：未核实具体日期。

DOI：https://doi.org/10.1016/j.jag.2024.104074

### 摘要

中文摘要要点（自行归纳），不冒充原文逐句译文。

这项方法根据树冠点云快速生成冠形相符的树模型。网络先生成分枝节点，图神经网络再预测节点属性与连接；结合最小生成树构成连通分枝图，最后生成树木网格。它用学习与图结构替代需要反复调参的程序化生长模拟。

### 流程、方法和效果

输入输出：树冠点云→分枝图→树木网格。

流程：树冠→节点网络→GNN→最小生成树→网格

方法：节点生成＋图学习＋连通性求解。

效果与条件：摘要报告平均每树建模从7 min降至＜0.5 s，未列计时硬件。

限制：冠形一致与视觉自然，不等于恢复实测树木的每根真实枝条。

粗读重点：看图结构及计时范围，区分条件生成与测量重建。

证据范围：效果主要依据摘要；未补造缺失数字。

来源核验：https://www.sciencedirect.com/science/article/pii/S156984322400428X；https://jszy.whu.edu.cn/ketao/en/lwcg/257133/content/66698.htm


## 07 AUPOME：上采样与网格提取

AUPOME: Unifying Anchor-guided UPsampling and octree mesh extraction for surface reconstruction

AUPOME：融合锚点引导上采样与八叉树网格提取的表面重建

作者：Jiangwei Sun；Rui Huang；Qingguang Li

出处：Pattern Recognition，2026，在线优先，114668。

2026-08-16首次在线；Journal Pre-proof；正式卷期未核实。

DOI：https://doi.org/10.1016/j.patcog.2026.114668

### 摘要

中文摘要要点（自行归纳），不冒充原文逐句译文。

AUPOME面向稀疏、带噪点云的表面重建，把上采样与网格提取放入同一框架。先以锚点和结构信息引导加密、细化多层特征，再用八叉树模块直接生成网格，以减少分阶段处理的误差传递，并关注拓扑与几何细节。

### 流程、方法和效果

输入输出：稀疏带噪点云→网格。

流程：点云→锚点引导加密→特征细化→八叉树网格

方法：结构引导上采样＋直接网格提取。

效果与条件：作者定性报告优于所比方法，摘要无具体数值。

限制：未核对完整实验表；2026在线预出版，正式卷期未确认。

粗读重点：核对联合流程、拓扑评价与加密倍率；倍率不是精度增幅。

证据范围：效果主要依据摘要；未补造缺失数字。

来源核验：https://www.sciencedirect.com/science/article/abs/pii/S0031320326016328


## 08 城市建筑轻量代理模型

Fast Building Instance Proxy Reconstruction for Large Urban Scenes

面向大规模城市场景的建筑实例代理模型快速重建

作者：Jianwei Guo；Haobo Qin；Yinchang Zhou；Xin Chen；Liangliang Nan；Hui Huang

出处：IEEE Transactions on Pattern Analysis and Machine Intelligence，2024，46(11)，7267–7282。

期刊卷期年：2024；首次在线：2024-04-16。

DOI：https://doi.org/10.1109/TPAMI.2024.3388371

### 摘要

完整摘要中译，原文来自用户上传IEEE题录。

大规模城市场景，尤其是建筑物的数字化，长期以来一直是一个尚未解决的问题，其原因在于数据采集面临多种挑战，例如场景覆盖不完整、缺少语义信息，以及路径规划的效率和可靠性较低。本文针对航空影像驱动的城市建筑重建中的这些挑战，提出了一套有效的流程和若干新算法，以高效地重建大规模城市场景中的三维建筑实例代理模型。具体来说，我们提出一种新的学习式方法，对航空影像中的城市建筑进行实例分割；随后，通过一个基于投票的算法，将多视角实例信息融合到稀疏点云中，该点云由标准的运动恢复结构（Structure from Motion，SfM）流程重建得到。我们的方法能够有效地从点云中分割出各个建筑实例。此外，我们还提出一种分层表面重建方法，专门用于从极其稀疏的点云中重建建筑物的三维代理模型。在大规模城市场景的合成航空影像和真实航空影像上开展的大量实验，证明了该方法的有效性。生成的场景代理模型已经能够为大规模城市场景中的建筑提供有用的三维表面表示；当这些具有实例信息的建筑代理模型用于航空路径规划时，能够显著提高数据的完整性和精度，从而得到细节丰富的三维建筑模型。

### 流程、方法和效果

输入输出：影像/SfM稀疏点云→轻量建筑代理；下游再次采集→精细模型。

流程：影像与SfM→实例投票到3D→分层代理建模→采集规划→精细重建

方法：二维实例学习＋SfM＋分层几何；建筑结构先验支撑轻量模型。

效果与条件：表6，Polytech：代理生成3.08 min，MVS Dense为487 min，均不含共同SfM的34.15 min。再次采集后的最终重建完整度（5 cm阈值）为49.77%与49.15%；这是最终精细模型的评价，不能当作代理精度。

限制：假设建筑可由堆叠棱柱表示，斜屋顶近似成平顶。此例90%误差为65.32 cm（MVS Dense 63.12 cm），并非全部精度更高。

粗读重点：看图2与§4–5；读表6和§6.5，分清代理与最终模型。

证据范围：已核对正文指定实验表/节选。

来源核验：https://ieeexplore.ieee.org/document/10499907；https://research.tudelft.nl/en/publications/fast-building-instance-proxy-reconstruction-for-large-urban-scene/


## 09 I-Filtering：保细节隐式距离场

I-Filtering: Implicit Filtering for Learning Neural Distance Functions From 3D Point Clouds

I-Filtering：从三维点云学习神经距离函数的隐式滤波

作者：Shengtao Li；Yudong Liu；Ge Gao；Ming Gu；Yu-Shen Liu

出处：IEEE Transactions on Pattern Analysis and Machine Intelligence，2026，48(1)，109–126。

期刊卷期年：2026；首次在线：2025-08-26。

DOI：https://doi.org/10.1109/TPAMI.2025.3602830

### 摘要

完整摘要中译，原文来自用户上传IEEE题录。

包括有符号距离函数（Signed Distance Function，SDF）和无符号距离函数（Unsigned Distance Function，UDF）在内的神经隐式函数，在拟合形状几何方面已经表现出很强的能力。然而，从离散、法向未定向的点云中推断连续距离场，仍然是一项挑战。神经网络通常会拟合出较粗糙的表面，并遗漏形状边缘、角点等细粒度几何细节。本文提出一种新的非线性隐式滤波器，在平滑隐式场的同时保留高频几何细节。我们的创新在于：利用邻近输入点以及有符号距离场的梯度，对表面，即零水平集，进行滤波。通过沿梯度方向移动原始输入点云，我们提出的隐式滤波还可以扩展到非零水平集，以保持不同水平集之间的一致性，从而更好地约束零水平集。由于无符号距离函数在零水平集处不可微，且缺少稳定的梯度场，我们进一步提出一种梯度不变训练方案，将该滤波器迁移到从点云学习的无符号距离函数上。借助这套 UDF 训练方案，我们也改善了稀疏视角重建的结果。我们在物体点云、复杂场景点云以及多视角影像的表面重建任务上开展了全面实验，并进一步将方法扩展到点法向估计和点云上采样任务。数值和可视化比较表明，在广泛使用的基准上，我们的方法优于已有的先进方法。

### 流程、方法和效果

输入输出：离散点云→SDF/UDF连续距离场→表面网格。

流程：邻域查询→距离场预测→梯度投影与隐式滤波→一致性优化→表面提取

方法：以保边滤波约束距离场，用非零水平集补充表面约束；UDF增加稳定梯度训练设计。

效果与条件：表I，FAMOUS：F-score为0.778（NeuralPull 0.746，阈值0.01）；L2 CD为0.008（0.100）。各表面采样10,000点评价；按论文尺度报告，不换算厘米。

限制：稀疏或邻域几何复杂时滤波可能不准；邻域处理增加训练成本；UDF分支使用LSUDF初始化并微调。

粗读重点：看图3–5、§III与表I；精读时再核对SDF/UDF梯度与§VIII局限。

证据范围：已核对正文指定实验表/节选。

来源核验：https://ieeexplore.ieee.org/document/11141752；https://yushen-liu.github.io/main/pdf/LiuYS_TPAMI25_IFiltering.pdf


## 10 Cloud2BIM：点云到IFC

Open-source automatic pipeline for efficient conversion of large-scale point clouds to IFC format

将大规模点云高效转换为IFC格式的开源自动化流程

作者：Slávek Zbirovský；Václav Nežerka

出处：Automation in Construction，2025，177，106303。

期刊卷期年：2025；首次在线：2025-06-09。

DOI：https://doi.org/10.1016/j.autcon.2025.106303

### 摘要

完整摘要中译，原文开放许可；见文末来源与许可。

建筑信息模型（BIM）的创建通常依赖繁重的人工工作：将激光扫描或摄影测量获得的非结构化点云数据转换成模型。本文提出开源软件工具Cloud2BIM，用于自动将点云转换为符合工业基础类（IFC）标准的BIM模型。Cloud2BIM集成了墙体和楼板分割、开口检测，以及基于真实墙面进行房间分区的先进算法，形成完整的全自动工作流程。与现有工具相比，它避开了RANSAC等计算和参数校准负担较重的技术，支持非正交几何结构，并提供了前所未有的处理速度，相比最快的竞争方案最高可快七倍。利用基准数据集开展的系统验证表明，Cloud2BIM是一种易用、高效、可扩展的精确BIM模型生成方案，能够在用户输入很少的情况下，将整栋建筑的大规模点云数据集转换为IFC格式。

### 流程、方法和效果

输入输出：输入：已扫描、配准且适当抽稀的室内/建筑点云（E57或XYZ，核心算法仅用xyz）；输出：含墙、楼板、门窗开口与房间空间实体的IFC参数化BIM。

流程：输入点云并控制采样密度，利用高度方向密度直方图分层和识别楼板。 → 将墙体线索投影为密度图，结合图像形态学、轮廓及线段操作提取墙面与墙厚。 → 连接墙段并处理空间关系，恢复实体墙体及房间区域。 → 分析墙面点密度直方图，识别门窗开口的位置和尺寸。 → 通过IfcOpenShell组织几何与语义实体，直接导出IFC。

方法：Cloud2BIM不是点云深度网络；以坐标密度和二维图像操作组织分层、墙体、开口和空间重建，支持非正交平面墙。Methods及代码说明直接支持上述流程。

效果与条件：Table9：ETH Zurich synth3（6,905,684点）连同IFC导出耗时60s；Kladno车站（2,551,721点）30s；Prague酒店（40,152,849点）30min。摘要声称最高7倍加速，正文对比涉及不同数据规模和他文硬件，不能视为统一基准上的精度排名。

限制：§3.4：暂不重建曲墙；门窗开口限矩形/正方形；楼层高度基本均一；稀疏点、遮挡或家具可能产生假开口，仍需BIM软件修正。精度评估主要点到模型距离和图示，部分GT本身不吻合，未给统一严格精度排名。

粗读重点：先看Fig.2整体流程，再看墙体如何变成有厚度实体和房间；浏览§2.10 IFC输出、Table9速度及§3.4局限。重点追踪分割结果如何继续变成BIM。

证据范围：已核对正文指定实验表/节选。

来源核验：https://arxiv.org/pdf/2503.11498v3；https://arxiv.org/abs/2503.11498


## 11 工程知识与参数化体积模型

From dense point clouds to semantic digital models: End-to-end AI-based automation procedure for Manhattan-world structures

从稠密点云到语义数字模型：面向曼哈顿世界结构的端到端AI自动化流程

作者：Mansour Mehranfar；Alexander Braun；André Borrmann

出处：Automation in Construction，2024，162，105392。

期刊卷期年：2024；首次在线：2024-03-23。

DOI：https://doi.org/10.1016/j.autcon.2024.105392

### 摘要

完整摘要中译，原文开放许可；见文末来源与许可。

本文提出一种新方法，可根据稠密点云数据，自动为曼哈顿环境中的建筑创建语义数字模型。与以往仅依靠数据驱动的方法不同，该方法将人工智能与工程领域知识结合，以克服复杂布局中室内点云处理和几何表达的困难。基于特征的决策树分类器提取主要建筑构件，并将这些构件用于基于知识的三维空间解析算法。在此基础上，优化过程生成参数化平面布局，最终用于创建体积数字模型。该方法在慕尼黑工业大学和斯坦福大学的数据集上得到验证，模型位置和构件参数估计的平均精度分别约为0.08米和0.06米，表明它能有效生成建筑的语义数字模型。这一方法展示了将人工智能融入数字孪生工作流程、实现更高程度自动化的潜力。

### 流程、方法和效果

输入输出：输入稠密建筑室内点云；输出含语义和几何的参数化建筑体积模型（曼哈顿世界假设，主体方向正交）。

流程：提取点云特征，通过决策树识别主要建筑构件。 → 结合工程知识进行三维空间解析，组织房间和构件关系。 → 优化参数化平面布局，确定几何参数。 → 据此构造有体积的语义数字模型。

方法：摘要明确决策树分类、基于知识的空间解析、参数化平面优化及体积建模；标题中的AI不是大模型或深度网络的同义词。

效果与条件：摘要在TUM及Stanford数据集上报告模型位置平均精度约0.08m、构件参数估计约0.06m。这里单位是米，不能误写成百分比准确率；具体统计公式和逐数据集分解需进一步查全文。

限制：曼哈顿世界假设限制一般非正交或曲面建筑；摘要未给完整误差定义及跨场景泛化统计。作者指出数据不可共享。

粗读重点：优先看自底向上识别与自顶向下工程知识怎样接合；再看平面布局优化如何支撑体积模型。

证据范围：效果主要依据摘要；未补造缺失数字。

来源核验：https://www.sciencedirect.com/science/article/pii/S0926580524001286；https://portal.fis.tum.de/en/publications/from-dense-point-clouds-to-semantic-digital-models-end-to-end-ai-/


## 12 少标签高架桥BIM

Semantic instance segmentation and automated 3D BIM reconstruction for viaduct using LiDAR point clouds and weakly-supervised learning

利用LiDAR点云与弱监督学习进行高架桥语义实例分割及自动三维BIM重建

作者：Zheng Qiao；Vincent J.L. Gan；Mingkai Li；Kelvin Goh Chun Keong；Lim Pia Lian；Allan Yeo Chen Long

出处：Automation in Construction，2026，181(Part A)，106612。

期刊卷期年：2026；首次在线：未核实具体日期。

DOI：https://doi.org/10.1016/j.autcon.2025.106612

### 摘要

中文摘要要点（自行归纳），不冒充原文逐句译文。

这篇文章把高架桥的少标签构件识别与参数化BIM生成相连。先用体素下采样协调点密度，弱监督分割后通过DBSCAN分离构件、过滤噪声，再依据构件形状和空间关系建模。分割评价与BIM几何评价分别衡量不同阶段。

### 流程、方法和效果

输入输出：高架桥LiDAR点云→参数化构件BIM。

流程：下采样→弱监督分割→实例聚类→参数化BIM

方法：少标签学习＋实例聚类＋几何规则。

效果与条件：表4：0.1%标签，OA 94.72%、mIoU 90.51%；摘要：10 mm容差下BIM准确性＞85%。

限制：数据保密；BIM“准确性”的具体计算式未核实。

粗读重点：读表4及构件参数生成；分割分数不是建模精度。

证据范围：已核对正文指定实验表/节选。

来源核验：https://www.sciencedirect.com/science/article/pii/S0926580525006521；https://www.sciencedirect.com/science/article/abs/pii/S0926580525006521


## 从这组论文看到的近期问题

以下是本组选文的线索，不是整个领域的热度统计。

| 问题 | 方法线索 | 对照阅读 |
|---|---|---|
| 稀疏、不均与缺失 | 输入条件生成、空间上下文、联合加密/提面 | 02、04、07 |
| 平滑与棱边细节冲突 | 距离场滤波、几何梯度和水平集约束 | 09 |
| 模型结构与可用性 | 线框、体块、图连接、参数化构件 | 01、03、06、11 |
| 多阶段误差传递 | 直接生成顶点/面，或联合上采样与网格提取 | 04、07 |
| 大场景效率 | 轻量代理、规则化BIM、快速结构生成 | 08、10、06 |
| 标注成本 | 弱监督构件识别与几何建模结合 | 12 |
| 几何与外观共同恢复 | 可见性约束、图割与纹理修补 | 05 |

生成模型不自动等于扩散模型；“AI”也可能指决策树等传统机器学习。神经网络既可用来预测标签，也可拟合连续距离场或生成几何连接，应根据输入输出辨认它承担哪一步。

## 哪些部分值得进一步认真看

只在准备继续做相关方向时精读。先选一条路线，不必把12篇都精读。

- 基础流程：10的总流程、IFC输出与限制；03的候选生成与优化；01的边缘—线框—面的转换。
- 隐式建模：09中SDF/UDF、零水平集、几何梯度与滤波约束，先理解表示，再看公式。
- 生成式建模：04的顶点/面生成及跨城训练设置；02的上下文模块消融；分清几何合理、水密和真实保真。
- 工程用途：11的知识假设，12的标签成本与几何评价，08的代理生成与最终精细重建两种结果。

## 粗读笔记模板

每篇写半页，允许标“未查”，不要凭标题补答案。

1. 任务与输入→输出是什么？
2. 流程分哪3–5步，本篇改变哪一步？
3. 主要先验来自几何规则、网络结构，还是辅助训练数据？
4. 一项效果证据：指标、数值、数据集、阈值/单位、基线与计时范围。
5. 一项限制：曲面/拓扑、稀疏缺失、跨域训练、资源或数据开放性。
6. 下一篇读什么，为什么？

## 小词表

| 术语 | 本轮需要知道的含义 |
|---|---|
| Surface / mesh | 连续表面／顶点和面连接形成的网格。 |
| Wireframe | 线框：结构边与连接，是模型的中间表示。 |
| Primitive / parametric model | 基元／参数模型：用平面、棱柱等及其参数描述几何。 |
| SDF / UDF | 有符号／无符号距离函数：对空间点预测到表面的距离。 |
| Level set / gradient | 水平集／梯度：等函数值的集合／函数局部变化方向。 |
| Autoregressive | 自回归：按已有序列逐步生成下一个顶点或面。 |
| Topology / watertight | 连接、洞与连通性／封闭无漏口；封闭不保证形状真实。 |
| SfM / MVS | 运动恢复结构／多视图立体：影像到稀疏／较稠密三维观测的常见步骤。 |
| BIM / IFC | 有语义与关系的工程信息模型／一种BIM交换标准。 |
| Manhattan-world | 主要方向正交的结构假设，不能任意推广到曲面与非正交建筑。 |
| GNN / MST | 图神经网络／最小生成树：学习节点与连接信息／构造连通树结构。 |
| CD / F-score | 距离相似性／阈值下精确与覆盖的综合评价；核对定义、尺度与阈值。 |



## 出处与译文依据


### [01] RR-Net: 3-D Roof Reconstruction From Airborne LiDAR Point Clouds via Edge Segmentation and Wireframe Generation

Yike Xu; Li Cao; Shengling Geng; Xiaoping Liu. IEEE Transactions on Geoscience and Remote Sensing, 2025, 63: 1–13. DOI: https://doi.org/10.1109/TGRS.2025.3625669

摘要处理：完整摘要中译，原文来自用户上传IEEE题录。

摘要来源：用户上传 export2026.10.09-04.52.45.csv，原记录 70。

https://yecoxu.github.io/

期刊卷期年：2025；首次在线：27 Oct 2025。

### [02] Integrating Spatial Context With Generative Model for Building Reconstruction From Airborne LiDAR Point Clouds

Yuxiang Zhao; Shengwen Li; Fang Fang; Nan Min; Sishi Gong; Yu Wang; Shunping Zhou. IEEE Transactions on Geoscience and Remote Sensing, 2026, 64: 1–13. DOI: https://doi.org/10.1109/TGRS.2026.3670027

摘要处理：完整摘要中译，原文来自用户上传IEEE题录。

摘要来源：用户上传 export2026.10.09-04.52.45.csv，原记录 198。

https://github.com/ShuaibZyx/SCGNet

期刊卷期年：2026；首次在线：3 Mar 2026。

### [03] A novel Building Section Skeleton for compact 3D reconstruction from point clouds: A study of high-density urban scenes

Yijie Wu; Fan Xue; Maosu Li; Sou-Han Chen. ISPRS Journal of Photogrammetry and Remote Sensing, 2024, 209: 85–100. DOI: https://doi.org/10.1016/j.isprsjprs.2024.01.020

摘要处理：中文摘要要点（自行归纳），不冒充原文逐句译文。

https://hub.hku.hk/handle/10722/340070

https://frankxue.com/pdf/wu24bss.pdf

https://www.sciencedirect.com/science/article/pii/S0924271624000297

期刊卷期年：2024；首次在线：未核实具体日期。

### [04] Point2Building: Reconstructing buildings from airborne LiDAR point clouds

Yujia Liu; Anton Obukhov; Jan Dirk Wegner; Konrad Schindler. ISPRS Journal of Photogrammetry and Remote Sensing, 2024, 215: 351–368. DOI: https://doi.org/10.1016/j.isprsjprs.2024.07.012

摘要处理：完整摘要中译，原文开放许可；见文末来源与许可。

许可：CC BY 4.0；以上中文为摘要翻译，非作者原始中文版本；https://creativecommons.org/licenses/by/4.0/。本册中文摘要为翻译改编，非作者审核译文。

https://arxiv.org/pdf/2403.02136v2

https://www.sciencedirect.com/science/article/pii/S092427162400279X

https://github.com/prs-eth/point2building

期刊卷期年：2024；首次在线：2024-07-26。

### [05] ColorMesh: Surface and texture reconstruction of large-scale scenes from unstructured colorful point clouds with adaptive automatic viewpoint selection

Mubai Li; Zhenxin Zhang; Siyun Chen; Liqiang Zhang; Zhihua Xu; Xiaoxu Ren; Jinlan Liu; Peng Sun. International Journal of Applied Earth Observation and Geoinformation, 2024, 132: 104041. DOI: https://doi.org/10.1016/j.jag.2024.104041

摘要处理：中文摘要要点（自行归纳），不冒充原文逐句译文。

https://www.sciencedirect.com/science/article/pii/S1569843224003959

https://doi.org/10.1016/j.jag.2024.104041

期刊卷期年：2024；首次在线：未核实具体日期。

### [06] Accelerated forest modeling from tree canopy point clouds via deep learning

Jiabo Xu; Zhili Zhang; Xiangyun Hu; Tao Ke. International Journal of Applied Earth Observation and Geoinformation, 2024, 132: 104074. DOI: https://doi.org/10.1016/j.jag.2024.104074

摘要处理：中文摘要要点（自行归纳），不冒充原文逐句译文。

https://www.sciencedirect.com/science/article/pii/S156984322400428X

https://jszy.whu.edu.cn/ketao/en/lwcg/257133/content/66698.htm

https://github.com/xujiabo/ForestCanopyToTree

期刊卷期年：2024；首次在线：未核实具体日期。

### [07] AUPOME: Unifying Anchor-guided UPsampling and octree mesh extraction for surface reconstruction

Jiangwei Sun; Rui Huang; Qingguang Li. Pattern Recognition, 2026, Online first: 114668. DOI: https://doi.org/10.1016/j.patcog.2026.114668

摘要处理：中文摘要要点（自行归纳），不冒充原文逐句译文。

https://www.sciencedirect.com/science/article/abs/pii/S0031320326016328

2026-08-16首次在线；Journal Pre-proof；正式卷期未核实。

### [08] Fast Building Instance Proxy Reconstruction for Large Urban Scenes

Jianwei Guo; Haobo Qin; Yinchang Zhou; Xin Chen; Liangliang Nan; Hui Huang. IEEE Transactions on Pattern Analysis and Machine Intelligence, 2024, 46(11): 7267–7282. DOI: https://doi.org/10.1109/TPAMI.2024.3388371

摘要处理：完整摘要中译，原文来自用户上传IEEE题录。

摘要来源：用户上传 export2026.10.09-04.52.45.csv，原记录 261。

https://ieeexplore.ieee.org/document/10499907

https://research.tudelft.nl/en/publications/fast-building-instance-proxy-reconstruction-for-large-urban-scene/

https://jianweiguo.net/publications/papers/2024-TPAMI-ProxyRecon.pdf

https://github.com/TalonX1/ProxyRecon

期刊卷期年：2024；首次在线：2024-04-16。

### [09] I-Filtering: Implicit Filtering for Learning Neural Distance Functions From 3D Point Clouds

Shengtao Li; Yudong Liu; Ge Gao; Ming Gu; Yu-Shen Liu. IEEE Transactions on Pattern Analysis and Machine Intelligence, 2026, 48(1): 109–126. DOI: https://doi.org/10.1109/TPAMI.2025.3602830

摘要处理：完整摘要中译，原文来自用户上传IEEE题录。

摘要来源：用户上传 export2026.10.09-04.52.45.csv，原记录 89。

https://ieeexplore.ieee.org/document/11141752

https://yushen-liu.github.io/main/pdf/LiuYS_TPAMI25_IFiltering.pdf

https://list17.github.io/ImplicitFilter

期刊卷期年：2026；首次在线：2025-08-26。

### [10] Open-source automatic pipeline for efficient conversion of large-scale point clouds to IFC format

Slávek Zbirovský; Václav Nežerka. Automation in Construction, 2025, 177: 106303. DOI: https://doi.org/10.1016/j.autcon.2025.106303

摘要处理：完整摘要中译，原文开放许可；见文末来源与许可。

许可：CC BY 4.0；论文©2025作者；中文为正式出版版摘要译文，未改变研究结论。；https://creativecommons.org/licenses/by/4.0/。本册中文摘要为翻译改编，非作者审核译文。

https://arxiv.org/pdf/2503.11498v3

https://arxiv.org/abs/2503.11498

https://github.com/VaclavNezerka/Cloud2BIM

期刊卷期年：2025；首次在线：2025-06-09。

### [11] From dense point clouds to semantic digital models: End-to-end AI-based automation procedure for Manhattan-world structures

Mansour Mehranfar; Alexander Braun; André Borrmann. Automation in Construction, 2024, 162: 105392. DOI: https://doi.org/10.1016/j.autcon.2024.105392

摘要处理：完整摘要中译，原文开放许可；见文末来源与许可。

许可：CC BY 4.0；论文©2024作者；中文为摘要译文。；https://creativecommons.org/licenses/by/4.0/。本册中文摘要为翻译改编，非作者审核译文。

https://www.sciencedirect.com/science/article/pii/S0926580524001286

https://portal.fis.tum.de/en/publications/from-dense-point-clouds-to-semantic-digital-models-end-to-end-ai-/

https://mediatum.ub.tum.de/doc/1738367/1738367.pdf

https://www.researchgate.net/publication/381070320_From_dense_point_clouds_to_semantic_digital_models_End-to-end_AI-based_automation_procedure_for_Manhattan-world_structures

期刊卷期年：2024；首次在线：2024-03-23。

### [12] Semantic instance segmentation and automated 3D BIM reconstruction for viaduct using LiDAR point clouds and weakly-supervised learning

Zheng Qiao; Vincent J.L. Gan; Mingkai Li; Kelvin Goh Chun Keong; Lim Pia Lian; Allan Yeo Chen Long. Automation in Construction, 2026, 181(Part A): 106612. DOI: https://doi.org/10.1016/j.autcon.2025.106612

摘要处理：中文摘要要点（自行归纳），不冒充原文逐句译文。

https://www.sciencedirect.com/science/article/pii/S0926580525006521

https://www.sciencedirect.com/science/article/abs/pii/S0926580525006521

https://cde.nus.edu.sg/dbe/staff/vincent-gan-dr/

https://www.rais4be.com/research

期刊卷期年：2026；首次在线：未核实具体日期。