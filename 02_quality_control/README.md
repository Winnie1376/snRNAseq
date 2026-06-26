# 质量控制模块

## 功能说明
此模块对单细胞RNA测序数据进行严格的质量控制，包括细胞过滤和双胞检测。

## 主要功能
- 基于UMI数、基因数、线粒体和叶绿体比例过滤细胞
- 使用DoubletFinder进行双胞检测和去除
- 标准化、降维和聚类分析
- 生成质控前后对比图
- 验证质控效果

## 文件列表
- `01.1QCtask.ipynb` - 主质控流程（包含双胞过滤）
- `01.2validateQCr.ipynb` - 质控结果验证

## 关键参数
- `minUMIs`: 最小UMI数（默认1000）
- `maxUMIs`: 最大UMI数（默认80000）
- `minGenes`: 最小基因数（默认500）
- `maxPercent.mt`: 最大线粒体比例（默认1%）
- `maxPercent.C`: 最大叶绿体比例（默认5%）
- `doublet.rate`: 双胞预期比例（默认0.05）

## 输出结果
- 质控后的RDS文件（`*_after_QC_doublet_filtered.rds`）
- DoubletFinder pK选择图
- 质控前后VlnPlot对比
- UMAP聚类图（按cluster和batch分组）

## 使用说明
1. 根据01_data_merge模块的质控图调整过滤参数
2. 运行01.1QCtask.ipynb进行质控
3. 运行01.2validateQCr.ipynb验证质控效果
4. 检查细胞保留率和质控后的数据分布
