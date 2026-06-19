# Visual-Cognitive-Engineering
choose question 1
# 基于视觉认知机制的植物抠图模型评测与失败案例分析

[cite_start]本项目为视觉认知工程课程，题目一的代码与认知挑战样本[cite: 229, 230, 231]。

[cite_start]植物图像由于包含细长茎秆、密集枝叶、内部孔洞以及极强的任务依赖性，被认为是底层视觉中非常具有挑战性的抠图场景 [cite: 3, 6][cite_start]。本项目选取了 ViTMatte、ZIM 和 Matting Anything 三个典型的抠图模型作为 Baseline 进行了系统评测 [cite: 3][cite_start]，系统归纳了主体识别、前景范围判断和边界预测等方面的失败案例（Failure Case），并从视觉认知机制的角度分析了其背后的深层原因 [cite: 3, 63, 79, 85]。在此基础上，本项目利用 Trimap 强先验辅助设计了后处理精修方案，使模型的测试指标得到了大幅优化。

---

## 📁 目录结构说明

根据测试需要和实验积累，本仓库的文件与数据目录结构如下（注：部分文件夹命名含当时手误敲错的字母，请以实际目录名为准）：

* [cite_start]**`addimage_resize/`**：自行补充构建的植物抠图认知挑战样本集（共 8 张，分辨率统一为 1024x1024），此文件夹存放 **RGB 原图** [cite: 14]。
* **`addiamges_alpharesize/`**：认知挑战样本集对应的 **Alpha 真实标注蒙版（Ground Truth）** [cite: 14]。
* **`addimages_trimap_resize/`**：利用真实 Alpha 蒙版腐蚀膨胀后，自动生成的对应 **Trimap（三分图）** 图像 [cite: 14, 122]。
* [cite_start]**`ViTMatte_compare/`**：ViTMatte 模型在认知挑战样本上的抠图效果可视化对比图 [cite: 3]。
* **`Matting-Anything_compare/`**：Matting Anything 模型在认知挑战样本上的抠图效果可视化对比图 [cite: 3]。
* **`ZIM_compare/`**：ZIM 模型在认知挑战样本上的抠图效果可视化对比图 [cite: 3]。
* **`trimap_create`**：用于从原始 Alpha 真实蒙版一键生成特定模型（如 ViTMatte）所需的 Trimap 辅助输入的 Python 脚本 [cite: 19, 122, 193]。
* **`evaluate`**：统一的测试集指标评估计算脚本。支持批量读取预测 Alpha 图与真实标签图，并统计输出全图的 MAE、MSE、SAD 评测指标 。
* **`trimap_post_processing`**：加分项对应的针对性改进脚本。利用自上而下的 Trimap 宏观认知先验，对 Matting Anything 和 ZIM 粗糙且不自信的初步预测结果进行硬校正与后处理精修。

---

## 🛠️ 核心脚本运行说明

### 1. 生成 Trimap 图像
[cite_start]在运行需要先验输入的抠图模型前，可运行此脚本根据真实的 Alpha 标签图批量生成未知区域较窄的精密三分图 [cite: 19, 122]：
```bash
python trimap_create
