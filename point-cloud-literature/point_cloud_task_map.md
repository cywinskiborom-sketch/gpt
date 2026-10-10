# 点云主流任务地图与全方向阅读入口

本次范围是点云相关的主要任务。建模和语义分割是用户举的例子，不是筛选边界。原745条已按点云相关性初筛，354条直接相关；其中按首次在线日期2024-10-10至2026-10-09限定后为225条。以下地图介绍这些样本涉及的主要任务，不是全领域热度排名，也不能据此保证检索完整。

原29篇清单是偏重重建、分割和配准的专项扩展名单。建议先看本地图，每类选一篇建立输入输出和流程概念，然后按兴趣扩展；不要求一次读完下面所有入口。

## 主要任务

| 任务 | 输入→输出 | 常规流程 | 常用评价 | 近期问题线索 | 样本入口 |
|---|---|---|---|---|---|
| 分类/识别 | 对象或场景点云→整份点云的类别 | 采样/增强→局部特征→全局聚合→分类头 | OA、平均类别准确率、各类准确率 | 少样本、损坏与旋转鲁棒性、跨域和开放类别 | [Efficient Point Cloud Processing With High-Dimensional Positional Encoding and Non-Local MLPs](https://doi.org/10.1109/TPAMI.2026.3665872)；[Towards Robust Point Cloud Recognition With Sample-Adaptive Auto-Augmentation](https://doi.org/10.1109/TPAMI.2025.3528392) |
| 语义/实例/全景分割 | 场景点云→逐点类别、对象实例或二者组合 | 分块/采样→点或体素特征→类别/实例掩码→恢复完整场景 | 语义mIoU；实例AP；全景PQ，分别比较 | 少标注、开放词汇、小对象、跨场景泛化 | [OpenUrban3D: Label-Free Open-Vocabulary Semantic Segmentation of Large-Scale Urban Point Clouds](https://doi.org/10.1109/TGRS.2026.3670962)；[Scalable SoftGroup for 3D Instance Segmentation on Point Clouds](https://doi.org/10.1109/TPAMI.2023.3326189)；[XMask3D++: Cross-Modal Mask Reasoning for Open Vocabulary 3D Segmentation](https://doi.org/10.1109/TPAMI.2026.3732036) |
| 3D目标检测 | 场景点云，可含图像→对象类别和三维框 | 点/体素/柱表示→特征提取→候选/查询/中心→框预测与筛选 | 3D AP、BEV AP；明确数据集、IoU阈值和距离 | 远距离稀疏目标、多模态、半监督、跨域 | [FSD V2: Improving Fully Sparse 3D Object Detection With Virtual Voxels](https://doi.org/10.1109/TPAMI.2024.3502456)；[SA3Det++: Side-Aware Quality Estimation for Semi-Supervised 3D Object Detection](https://doi.org/10.1109/TPAMI.2025.3594086) |
| 配准/定位/SLAM | 两组或连续扫描→刚体变换、位姿和地图 | 配准：匹配→鲁棒变换→精化；SLAM：时序前端→地图→回环/后端（依系统） | 配准旋转/平移误差和召回；SLAM轨迹ATE/RPE | 低重叠、异源扫描、动态物体、跨尺度、长期定位 | [Consistency-Aware Spot-Guided Transformer for Accurate and Versatile Point Cloud Registration](https://doi.org/10.1109/TPAMI.2026.3653989)；[ATCM: Aerial–Terrestrial LiDAR-Based Collaborative Simultaneous Localization and Mapping](https://doi.org/10.1109/TGRS.2025.3563358)；[Toward Zero-Shot Point Cloud Registration Across Diverse Scales, Scenes, and Sensor Setups](https://doi.org/10.1109/TPAMI.2026.3722524) |
| 表面/结构重建与建模 | 观测点云→曲面、网格、线框或参数化结构模型 | 清理/对齐→邻域或法向→曲面估计或构件拟合→模型提取/检查 | 精度/完整度、CD、F-score；结构参数和拓扑 | 真实扫描缺陷、大场景、结构约束、细节保留 | [A Survey and Benchmark of Automatic Surface Reconstruction From Point Clouds](https://doi.org/10.1109/TPAMI.2024.3510932)；[RR-Net: 3-D Roof Reconstruction From Airborne LiDAR Point Clouds via Edge Segmentation and Wireframe Generation](https://doi.org/10.1109/TGRS.2025.3625669)；[AdLeaf: Quantitative Leaf Reconstruction From TLS Point Clouds](https://doi.org/10.1109/TGRS.2025.3608325) |
| 点云补全 | 残缺点云→包含缺失几何的完整预测 | 可见点编码→粗形状推断→几何细化→保真与完整度评测 | CD、阈值F-score，有时EMD；统一采样口径 | 真实遮挡、未见类别、合理形状与可见部分保真 | [ProtoComp++: Diverse Point Cloud Completion With Controllable Prototype](https://doi.org/10.1109/TPAMI.2026.3674197)；[Flexible-Weighted Chamfer Distance: Enhanced Objective Function for Point Cloud Completion](https://doi.org/10.1109/TPAMI.2026.3669003) |
| 几何预处理：去噪/法向/上采样 | 含噪或稀疏点云→干净点云、法向或密集点云 | 邻域构造→几何估计/学习→修正位置、预测法向或新增点→几何检查 | 点到曲面距离/CD；法向角误差；细节和分布 | 未知噪声、密度不均、边缘保留、真实扫描 | [Progressive Point Cloud Denoising Guided by Unsigned Distance Function](https://doi.org/10.1109/TGRS.2026.3696434)；[PointNorm-Net: Self-Supervised Normal Prediction of 3D Point Clouds via Multi-Modal Distribution Estimation](https://doi.org/10.1109/TPAMI.2025.3562051)；[I-Filtering: Implicit Filtering for Learning Neural Distance Functions From 3D Point Clouds](https://doi.org/10.1109/TPAMI.2025.3602830) |
| 点云几何/属性压缩 | 点坐标及颜色等属性→码流→解码点云 | 空间划分/潜变量→预测与量化→熵编码→解码 | 码率、D1/D2几何失真、属性失真、率失真曲线/BD-rate | 动态编码、低延迟、学习式概率模型、统一有损/无损 | [Deep Learning-Based Point Cloud Compression: An In-Depth Survey and Benchmark](https://doi.org/10.1109/TPAMI.2025.3594355)；[Next Bit Prediction: A Unified Lossless and Lossy Point Cloud Geometry Compression Framework](https://doi.org/10.1109/TPAMI.2025.3650590) |
| 连续点云：场景流/跟踪/预测 | 多帧点云→逐点运动、对象轨迹或未来状态 | 时序特征/对应→运动估计、对象关联或未来预测 | 场景流EPE3D；单目标跟踪Success/Precision；多目标HOTA/IDF1；未来点云CD | 遮挡、非刚性运动、时序关联、预测不确定性 | [Sequential Point Clouds: A Survey](https://doi.org/10.1109/TPAMI.2024.3365970)；[DifFlow3D: Hierarchical Diffusion Models for Uncertainty-Aware 3D Scene Flow Estimation](https://doi.org/10.1109/TPAMI.2025.3629570)；[Revisiting Siamese-Based 3D Single Object Tracking With a Versatile Transformer](https://doi.org/10.1109/TPAMI.2025.3581381) |
| 三维变化检测 | 同一区域不同时间点云→变化位置、对象或语义类别 | 跨期对齐→尺度/密度协调→几何或语义差异→变化判定 | 变化类别IoU、F1、精确率/召回率 | 配准造成的假变化、遮挡/季节差异、类别不均衡 | [Ms-DANet: Multiscale Difference-Aware Network for 3-D Point Cloud Change Detection](https://doi.org/10.1109/TGRS.2025.3549492)；[ME-CPT: Multitask Enhanced Cross-Temporal Point Transformer for Urban 3-D Change Detection](https://doi.org/10.1109/TGRS.2026.3661736) |

## 概念边界

- 整体分类预测整份对象/场景点云的类别；逐点地物分类属于语义分割。语义、实例、全景分割具有不同输出与指标。
- 配准主要估计整体刚体变换；场景流估计逐点运动，可能包含多个对象和非刚性运动。定位/SLAM还包含时序状态与地图管理。
- 重建依据观测恢复几何。文本、图像或先验驱动的三维生成可另列邻近任务，需核对是否以点云作为核心研究对象。
- 压缩坐标和属性数据属于点云压缩；神经网络剪枝/量化属于模型效率方法，云边特征压缩也需另行标明。
- 去噪、法向估计、上采样在这里归为几何预处理，但可独立研究。I-Filtering的主任务是点云到隐式距离场/表面重建，法向和上采样是扩展应用。
- 原全量表的任务列使用较粗标签，部分场景流、跟踪、变化检测和法向工作置于“其他”。它们已保留在相关性池；可通过本地图的题目、DOI或原始记录号定位。

## 横向方法单独记录

自监督/预训练、少标注/弱监督、多模态、域适应/泛化、开放词汇、Transformer/Mamba、生成扩散、隐式表示等可用于多个任务。它们应另记为方法或训练设置，不能与上述任务混排数量。PonderV2、SPOT、标签高效学习综述可作为跨任务背景。

## 全方向起步阅读

表中日期为用户CSV的Online Date；窗口外条目明确作为基础补读。推荐基于题名和摘要，全文实验仍需核对。

| 入口 | 任务 | 文献 | 首次在线 | 粗读重点 |
|---|---|---|---|---|
| 1（原始记录95） | 分类/识别 | [Efficient Point Cloud Processing With High-Dimensional Positional Encoding and Non-Local MLPs](https://doi.org/10.1109/TPAMI.2026.3665872) | 2026-02-17；近两年 | 从局部特征到全局聚合与分类头；与逐点分割头对照。 |
| 2（原始记录57） | 语义分割 | [OpenUrban3D: Label-Free Open-Vocabulary Semantic Segmentation of Large-Scale Urban Point Clouds](https://doi.org/10.1109/TGRS.2026.3670962) | 2026-03-05；近两年 | 点云渲染、视觉语言特征和点云蒸馏如何服务于逐点预测。 |
| 3（原始记录167） | 实例分割 | [Scalable SoftGroup for 3D Instance Segmentation on Point Clouds](https://doi.org/10.1109/TPAMI.2023.3326189) | 2023-10-20；窗口外：基础补读 | 软语义预测→点分组→实例精化，区分类别和对象编号。 |
| 4（原始记录273） | 3D目标检测 | [FSD V2: Improving Fully Sparse 3D Object Detection With Virtual Voxels](https://doi.org/10.1109/TPAMI.2024.3502456) | 2024-11-19；近两年 | 点云稀疏编码→虚拟体素→中心特征与目标分配→三维框。 |
| 5（原始记录124） | 配准 | [Consistency-Aware Spot-Guided Transformer for Accurate and Versatile Point Cloud Registration](https://doi.org/10.1109/TPAMI.2026.3653989) | 2026-01-14；近两年 | 特征→粗对应→精对应→变换估计；关注一致性和重叠率。 |
| 6（原始记录344） | SLAM | [ATCM: Aerial–Terrestrial LiDAR-Based Collaborative Simultaneous Localization and Mapping](https://doi.org/10.1109/TGRS.2025.3563358) | 2025-04-22；近两年 | 单机器人前端→跨视角回环→全局位姿图优化。 |
| 7（原始记录92） | 表面重建 | [A Survey and Benchmark of Automatic Surface Reconstruction From Point Clouds](https://doi.org/10.1109/TPAMI.2024.3510932) | 2024-12-04；近两年 | 传统/学习先验、输入缺陷、真实扫描鲁棒性和精度。 |
| 8（原始记录5） | 点云补全 | [ProtoComp++: Diverse Point Cloud Completion With Controllable Prototype](https://doi.org/10.1109/TPAMI.2026.3674197) | 2026-03-16；近两年 | 原型粗生成→几何细化；语言提示与真实扫描基准。 |
| 9（原始记录161） | 去噪 | [Progressive Point Cloud Denoising Guided by Unsigned Distance Function](https://doi.org/10.1109/TGRS.2026.3696434) | 2026-05-25；近两年 | 噪声点→中间位置→位移距离/方向→曲面；核对监督来源。 |
| 10（原始记录29） | 点云压缩 | [Next Bit Prediction: A Unified Lossless and Lossy Point Cloud Geometry Compression Framework](https://doi.org/10.1109/TPAMI.2025.3650590) | 2026-01-05；近两年 | 几何符号概率、占据与坐标残差；区分码率和重建失真。 |
| 11（原始记录430） | 场景流 | [DifFlow3D: Hierarchical Diffusion Models for Uncertainty-Aware 3D Scene Flow Estimation](https://doi.org/10.1109/TPAMI.2025.3629570) | 2025-11-06；近两年 | 连续时刻点云→层级条件扩散→逐点位移和不确定性。 |
| 12（原始记录129） | 变化检测 | [Ms-DANet: Multiscale Difference-Aware Network for 3-D Point Cloud Change Detection](https://doi.org/10.1109/TGRS.2025.3549492) | 2025-03-10；近两年 | 双云编码→多尺度差异→融合→逐点变化类别。 |
| 13（原始记录51） | 法向估计 | [PointNorm-Net: Self-Supervised Normal Prediction of 3D Point Clouds via Multi-Modal Distribution Estimation](https://doi.org/10.1109/TPAMI.2025.3562051) | 2025-04-16；近两年 | 三阶段法向分布估计、减少法向标注和真实域泛化。 |
| 14（原始记录267） | 单目标跟踪 | [Revisiting Siamese-Based 3D Single Object Tracking With a Versatile Transformer](https://doi.org/10.1109/TPAMI.2025.3581381) | 2025-06-19；近两年 | 模板点云→搜索区域匹配→目标位置与朝向；与场景流区分。 |
| 15（原始记录247） | 横向方法：预训练 | [PonderV2: Improved 3D Representation With a Universal Pre-Training Paradigm](https://doi.org/10.1109/TPAMI.2025.3561598) | 2025-04-18；近两年 | 3D编码器→可微渲染监督→迁移到分割、检测、重建等任务。 |
| 16（原始记录16） | 点云压缩 | [Deep Learning-Based Point Cloud Compression: An In-Depth Survey and Benchmark](https://doi.org/10.1109/TPAMI.2025.3594355) | 2025-07-31；近两年 | 几何/属性、有损/无损、码率失真及标准。 |
| 17（原始记录2） | 连续点云 | [Sequential Point Clouds: A Survey](https://doi.org/10.1109/TPAMI.2024.3365970) | 2024-02-14；窗口外：基础补读 | 场景流、检测跟踪、分割和预测的4D任务地图。 |

每篇最后写清：输入输出、具体问题、完整流程、相对基线改动、监督/数据/指标、代价与局限。
