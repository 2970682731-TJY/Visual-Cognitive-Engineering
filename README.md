# Visual-Cognitive-Engineering
choose question 1
# 基于视觉认知机制的植物抠图模型评测与失败案例分析

[本项目为视觉认知工程课程，题目一的代码与认知挑战样本。

植物图像由于包含细长茎秆、密集枝叶、内部孔洞以及任务依赖性，被认为是底层视觉中具有挑战性的抠图场景。本项目选取了ViTMatte、ZIM和Matting Anything三个典型的抠图模型作为Baseline进行了评测，归纳了主体识别、前景范围判断和边界预测等方面的失败案例，并从视觉认知机制的角度分析了其背后的原因。在此基础上，本项目利用Trimap先验辅助设计了后处理方案，使模型的测试指标得到了优化。

---

## 📁 目录结构说明

根据测试需要和实验积累，本仓库的文件与数据目录结构如下（注：部分文件夹命名含当时手误敲错的字母，请以实际目录名为准）：

* **`addimage_resize/`**：自行补充构建的植物抠图认知挑战样本集（共8张，分辨率统一为1024x1024），此文件夹存放 **RGB 原图** 。
* **`addiamges_alpharesize/`**：认知挑战样本集对应的 **Alpha 真实标注蒙版（Ground Truth）** 。
* **`addimages_trimap_resize/`**：利用真实Alpha蒙版腐蚀膨胀后，生成的对应 **Trimap（三分图）** 图像。
* **`ViTMatte_compare/`**：ViTMatte模型在认知挑战样本上的抠图效果可视化对比图。
* **`Matting-Anything_compare/`**：Matting Anything模型在认知挑战样本上的抠图效果可视化对比图。
* **`ZIM_compare/`**：ZIM模型在认知挑战样本上的抠图效果可视化对比图。
* **`trimap_create`**：用于从原始Alpha真实蒙版生成特定模型（ViTMatte）所需的Trimap辅助输入的Python脚本。
* **`evaluate`**：统一的测试集指标评估计算脚本。支持读取预测Alpha图与真实标签图，并统计输出全图的MAE、MSE、SAD评测指标 。
* **`trimap_post_processing`**：加分项对应的针对性改进脚本。利用Trimap认知先验，对Matting Anything和ZIM的预测结果进行后处理。

---
