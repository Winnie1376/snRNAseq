# 细胞类型注释模块

## 功能说明
此模块使用marker基因进行细胞类型注释，生成可视化结果帮助识别细胞类型。

## 主要功能
- 基于marker基因列表进行细胞类型识别
- 基因ID自动匹配和标准化
- 生成DotPlot、VlnPlot和FeaturePlot
- 自动调整图片尺寸以适应marker数量

## 文件列表
- `03.1annotationTask.ipynb` - Marker基因可视化主脚本
- `03.2AnnoGeneListTask.ipynb` - Marker基因列表管理

## 输入数据格式
Marker文件应包含以下列（制表符分隔）：
- `Gene_ID`: 基因ID
- `Name`: 基因名称
- `Summarized_Info`: 细胞类型或功能描述

示例：
```
Gene_ID         Name    Summarized_Info
AT1G65330       PHE1    CZE
AT1G65300       PHE2    CZE
AT1G49770       ZOU     ESR
```

## 输出结果
- `*_marker_DotPlot.pdf` - 点图（表达量和表达比例）
- `*_marker_VlnPlot.pdf` - 小提琴图（表达分布）
- `*_marker_FeaturePlot.pdf` - UMAP特征图（可选）

## 使用说明
1. 准备marker基因列表文件（TSV格式）
2. 设置参数：
   - `prefix`: 样本名称
   - `rds_path`: 质控后的RDS文件路径
   - `marker_file`: Marker基因列表路径
   - `output_dir`: 输出目录
3. 运行03.1annotationTask.ipynb
4. 根据DotPlot和VlnPlot结果识别各cluster的细胞类型
5. 使用03.2AnnoGeneListTask.ipynb管理和更新marker基因列表

## 注意事项
- 脚本会自动将基因ID转换为大写进行匹配
- 如果marker基因未找到，会输出警告信息
- 图片尺寸会根据marker数量和cluster数量自动调整
