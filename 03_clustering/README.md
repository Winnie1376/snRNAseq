# 聚类分析模块

## 功能说明
此模块负责优化聚类参数、确定最佳分辨率，并评估聚类质量和批次效应。

## 主要功能
- Resolution参数优化
- Clustree可视化聚类稳定性
- Elbow plot确定最佳PCA维度
- 按cluster和批次展示质控指标
- 聚类与批次相关性分析

## 文件列表
- `02.1resolutionTask.ipynb` - Resolution优化和clustree分析
- `02.2reclusterTask.ipynb` - 使用最佳参数重新聚类
- `02.3vlnQCbyClustersTask.ipynb` - 按cluster展示QC指标
- `02.4QC_correlation_Batch.ipynb` - 聚类与批次相关性分析
- `02.4VlnQCbyClasses.ipynb` - 按细胞类型展示QC指标

## 关键参数
- `resolution`: 聚类分辨率（建议范围0.1-2.0）
- `dim.usage`: PCA维度数（根据Elbow plot确定）

## 输出结果
- Cluster number图（resolution vs 聚类数）
- Clustree图（聚类稳定性）
- Elbow plot（PCA维度选择）
- 各cluster的质控指标分布图
- 聚类与批次的相关性热图

## 使用说明
1. 运行02.1resolutionTask.ipynb，观察cluster number和clustree图
2. 根据聚类稳定性选择最佳resolution
3. 运行02.2reclusterTask.ipynb使用最佳参数重新聚类
4. 运行02.3和02.4脚本评估聚类质量和批次效应
5. 如果发现严重批次效应，考虑使用整合方法（Harmony/Seurat Integration）
