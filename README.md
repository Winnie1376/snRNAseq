# snRNAseq 单细胞RNA测序分析流程

植物单细胞RNA测序数据分析完整流程，适用于拟南芥等植物物种。

## 项目结构

```
snRNAseq/
├── 01_data_merge/          # 数据合并
├── 02_quality_control/     # 质量控制
├── 03_clustering/          # 聚类分析
└── 04_annotation/          # 细胞类型注释
```

## 分析流程

### 1. 数据合并 (`01_data_merge/`)
- 读取10X Genomics格式数据
- 合并多个样本
- 计算线粒体/叶绿体基因比例
- 生成初步质控图

**输出**: `*_merge_raw.rds`

### 2. 质量控制 (`02_quality_control/`)
- 细胞过滤（UMI数、基因数、线粒体/叶绿体比例）
- DoubletFinder双胞检测和去除
- 标准化和降维
- 质控效果验证

**输出**: `*_after_QC_doublet_filtered.rds`

### 3. 聚类分析 (`03_clustering/`)
- Resolution参数优化
- Clustree聚类稳定性评估
- 批次效应检查
- 最佳参数重聚类

**输出**: Cluster图、Clustree图、Elbow plot

### 4. 细胞类型注释 (`04_annotation/`)
- Marker基因可视化
- DotPlot/VlnPlot/FeaturePlot
- 细胞类型识别

**输出**: Marker基因表达图

## 快速开始

### 环境要求
- R ≥ 4.0
- Seurat
- DoubletFinder
- clustree
- ggplot2, dplyr

### 运行流程
```bash
# 1. 数据合并
jupyter notebook 01_data_merge/00mergeTask.ipynb

# 2. 质量控制
jupyter notebook 02_quality_control/01.1QCtask.ipynb

# 3. 聚类分析
jupyter notebook 03_clustering/02.1resolutionTask.ipynb

# 4. 细胞类型注释
jupyter notebook 04_annotation/03.1annotationTask.ipynb
```

## 关键参数

| 参数 | 默认值 | 说明 |
|------|--------|------|
| minUMIs | 1000 | 最小UMI数 |
| maxUMIs | 80000 | 最大UMI数 |
| minGenes | 500 | 最小基因数 |
| maxPercent.mt | 1% | 最大线粒体比例 |
| maxPercent.C | 5% | 最大叶绿体比例 |
| doublet.rate | 0.05 | 双胞预期比例 |
| resolution | 0.5 | 聚类分辨率 |
| dim.usage | 20 | PCA维度数 |

## 输出文件说明

| 文件类型 | 说明 |
|---------|------|
| `*.rds` | Seurat对象（R数据文件） |
| `*_VlnPlot.pdf` | 小提琴图（质控指标分布） |
| `*_DotPlot.pdf` | 点图（marker基因表达） |
| `*_UMAP.pdf` | UMAP降维图 |
| `*.cluster_tree.pdf` | Clustree聚类稳定性图 |

## 分析建议

1. **质控参数调整**: 根据01_data_merge的质控图确定过滤阈值
2. **Resolution选择**: 观察clustree图，选择稳定的resolution值
3. **批次效应**: 如发现严重批次效应，考虑使用Harmony或Seurat Integration
4. **Marker基因**: 根据物种和组织类型准备合适的marker基因列表

## 常见问题

**Q: 如何判断质控参数是否合适？**
A: 检查质控后细胞保留率（建议≥70%），观察VlnPlot确保去除了低质量细胞。

**Q: 如何选择最佳resolution？**
A: 结合cluster number图和clustree图，选择聚类数量合理且节点稳定的resolution。

**Q: 双胞过滤效果如何验证？**
A: 观察DoubletFinder pK选择图和双胞比例（应接近设定值5%）。

## 引用

如果使用本流程，请引用相关工具：
- Seurat: Hao et al. (2021) Cell
- DoubletFinder: McGinnis et al. (2019) Cell Systems
- clustree: Zappia and Oshlack (2018) GigaScience

## 许可证

MIT License

## 联系方式

- GitHub: https://github.com/Winnie1376/snRNAseq
- Issues: 欢迎提交问题和建议
