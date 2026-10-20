# Luggage Damage Datasets

本仓库按数据集整理现有行李箱图片及标注，包含 **DLSD** 和 **OLCD**。当前未提供 ADLD，不以其他数据代替。

## DLSD

箱体表面破损检测，保留原始训练/验证划分。

| 划分 | 图片 | YOLO 标注文件 |
| --- | ---: | ---: |
| train | 2626 | 2626 |
| val | 657 | 657 |
| 合计 | 3283 | 3283 |

类别编号：`0 scratch`、`1 rupture`、`2 hollow`、`3 deformation`。图片位于 `DLSD/images/{train,val}`，标注位于 `DLSD/labels/{train,val}`。

`DLSD/supplemental_hollow/` 单独保留原 hollow 目录的补充图片及 XML/TXT 标注（200 张图片）。其中 81 张与主 DLSD 图片内容相同；该目录不计入上表，也未合并进原始训练/验证集。

## OLCD

行李组件检测，按原 Good、Bad、Good_Bad 分别整理为 Normal、Challenge、Whole。

| 子集 | train | val | 合计 |
| --- | ---: | ---: | ---: |
| Normal | 868 | 218 | 1086 |
| Challenge | 733 | 185 | 918 |
| Whole | 1595 | 403 | 1998 |

各子集使用 `images/{train,val}` 和 `labels/{train,val}` 目录。YOLO 类别编号：`0 wheel`、`1 lock`、`2 handle`、`3 box`、`4 lever`。

每个子集保留既有划分；Whole 是原始合并版本，并未根据 Normal 和 Challenge 重新合并。原始两组子集共 2004 份标注，Whole 为 1998 份，保留这一差异。Normal 和 Whole 各有一个内容完全相同的 `.jpg`/`.jpeg` 副本，整理时仅保留 `.jpg`。

`annotations_original/` 保留原 COCO JSON，不作为本仓库图片数量的统计依据；原 JSON 存在图片记录与现存文件不完全一致的情况。`Normal/annotations_normal_subset/` 保留“正常行李组件标注”目录中 324 份 XML 和 324 份 TXT 原标注；该目录的 325 张原图片已全部包含在 Normal 中，不重复存图。此处原标注未改动，类别映射应按原格式单独核对。

## 使用

DLSD 及 OLCD 各子集提供 `classes.txt` 和 `data.yaml`，用于主 YOLO 标注。使用时将 `data.yaml` 中的 `path` 改为相应数据集目录的绝对路径。

本仓库未包含论文 PDF、训练缓存及原始压缩包；未修改原始图片与标注内容，未重新划分数据。
