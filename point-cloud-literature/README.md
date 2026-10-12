# 点云文献筛选与阅读材料

这份材料来自 745 条 TGRS / TPAMI 题录，依据题名、作者关键词和摘要进行初筛，未逐篇阅读全文。推荐项核对了摘要；模态不明确的条目保留为待核验。

## 范围与全方向入口

建模和语义分割只是举例，本次覆盖点云的主要任务。先看[任务地图与全方向阅读入口](point_cloud_task_map.md)，包括分类、语义/实例分割、3D检测、配准/SLAM、重建、补全、几何预处理、压缩、连续点云和变化检测。自监督/预训练、多模态、泛化与架构单独作为横向方法。

## 下载后先打开哪个文件

| 文件 | 用途 |
|---|---|
| [point_cloud_screening.xlsx](point_cloud_screening.xlsx) | 推荐先打开。包含全方向任务地图、17个起步入口、29篇专项扩展、近两年直接相关池、745条初筛、原始题录及笔记模板 |
| [point_cloud_screening.csv](point_cloud_screening.csv) | 保留原始字段并加入相关性、任务、理由和日期标记，便于导入其他软件 |
| [point_cloud_review.md](point_cloud_review.md) | 筛选依据、对原AI回复的修正、常规流程与阅读建议，可直接在GitHub阅读 |

Excel先看“任务地图（全方向）”和“全方向起步阅读”，每类先选一篇；原29篇放在“阅读顺序与重点”作为专项扩展，随后按兴趣进入“近两年直接相关”。“全量初筛745”可以按相关性、日期与任务过滤。

## 结果与日期口径

- 原始记录：745条；TGRS 412、TPAMI 333；出版年覆盖2024–2026。
- 全量初筛：直接相关354、邻近相关274、当前排除101、待核验16。
- 以CSV的Online Date为准，暂按导出日前24个月：2024-10-10至2026-10-09，共492条，其中直接相关225条。
- 若按出版年2025–2026统计，则原始候选为487条，两种日期口径不能混用。
- 任务标签可多选，数量不能相加。直接相关包含少量影像/传感器数据生成点云的研究；它们与扫描点云输入的方法具有不同流程。
- 相关性判断和阅读优先级可在全文阅读后修改；本文件不能证明检索完整或代表全领域热度。

## GitHub怎么用

GitHub仓库保存文件和修改历史。阅读成果可以直接在仓库网页下载：

1. 返回[仓库首页](https://github.com/cywinskiborom-sketch/gpt)，点击绿色 **Code → Download ZIP**。
2. 解压后进入 `point-cloud-literature`，用Excel打开 `point_cloud_screening.xlsx`。
3. 也可以点开单个文件，再点击下载原始文件的按钮。
4. Markdown说明可以直接在GitHub网页阅读。

[GitHub官方下载说明](https://docs.github.com/zh/repositories/working-with-files/using-files/downloading-files-from-github)

## Codespaces怎么用

Codespaces是一台在线运行代码的云电脑，会克隆仓库；本次上传通过ChatGPT已授权的GitHub连接完成。连接GitHub、打开Codespaces、当前聊天的执行环境是不同的连接关系。

1. 在仓库首页选择 `main`，点击 **Code → Codespaces**。打开已有环境，或创建一个codespace。
2. 左侧文件栏可查看仓库文件；终端可运行代码。阅读Excel可以先下载到本地。
3. 修改仓库文件后，在编辑器的Source Control（源代码管理）中检查变更，填写说明并 **Commit（提交）**，再 **Push（推送）** 到GitHub；仓库保存的是已经推送的版本。
4. 用完打开[Codespaces列表](https://github.com/codespaces)，在对应环境右侧点 **… → Stop codespace**。仅关闭浏览器标签页不会立即停止运行。停止后仍保留环境和存储；计算及存储额度以账号页面为准。

[创建Codespace](https://docs.github.com/zh/codespaces/developing-in-a-codespace/creating-a-codespace-for-a-repository?tool=webui) · [官方入门](https://docs.github.com/zh/codespaces/quickstart) · [停止与启动](https://docs.github.com/zh/codespaces/developing-in-a-codespace/stopping-and-starting-a-codespace?tool=webui)

## 后续读论文怎么记

每篇记录：输入→输出；具体瓶颈；完整流程及相对基线改动；监督与数据划分；指标、基线和消融；计算代价、适用条件与失败情形。

建议给导师的成果：任务地图，建模和语义分割各一张流程图，以及每个主要任务2–3篇近期代表作对照。

## 综述中文译稿与导读

已提供 *Surface Reconstruction From Point Clouds: A Survey and a Benchmark* 的中文译稿 PDF 与独立粗读导读，保留原图表及公式，并按原文页码导航。

[打开译稿与导读文件夹](surface-reconstruction/README.md)。建议先看 7 页导读，再按需查阅 36 页译稿。

## 2024–2026 点云建模典型论文

[打开六刊建模阅读册](modeling-2024-2026/README.md)：12篇论文，19页PDF，包含中文摘要、出处、常规流程、方法、效果证据与粗读重点。7篇完整摘要中译、5篇中文摘要要点，分别标注来源；2026在线优先论文单列状态。
