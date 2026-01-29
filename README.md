# HUST-OBC 甲骨文数据集（教学精简版）

本仓库包含用于AI识别甲骨文教学演示的精简数据集和预训练模型。

## 资源说明

### 数据集

| 项目 | 数值 |
|------|------|
| 字符类别 | 150 |
| 图片总数 | 1,200 |
| 每类图片 | 约8张 |
| 文件大小 | 5.4 MB |

### 预训练模型

| 项目 | 说明 |
|------|------|
| 模型 | ResNet50 |
| 文件 | max_val_acc.pth |
| 大小 | 204.53 MB |
| 准确率 | 94.6% |

## 数据来源

本数据集和模型来自 **HUST-OBC**（华中科技大学甲骨文字符数据集），仅用于教学演示目的。

原始数据集信息：
- 论文：Wang P, et al. An open dataset for oracle bone script recognition and decipherment. *Scientific Data*, 2024.
- GitHub：https://github.com/Pengjie-W/HUST-OBC
- DOI：https://doi.org/10.6084/m9.figshare.25040543

## 目录结构
```
HUST-OBC-Mini/
└── deciphered/
    ├── 1/                    # 字符类别ID
    │   ├── X_1_xxx.png       # 甲骨文图片
    │   └── L_1_xxx.png
    ├── 2/
    │   └── ...
    ├── ID_to_chinese.json    # ID -> 现代汉字 映射
    └── chinese_to_ID.json    # 现代汉字 -> ID 映射
```

## 下载链接

- 数据集：[HUST-OBC-Mini.zip](https://github.com/zhaoyanghao125-sudo/oracle-bone-teaching/releases/download/MINI/HUST-OBC-Mini.zip)
- 模型：[max_val_acc.pth](https://github.com/zhaoyanghao125-sudo/oracle-bone-teaching/releases/download/model/max_val_acc.pth)

## 使用方法

### 在Google Colab中下载
```python
# 下载数据集
!wget https://github.com/zhaoyanghao125-sudo/oracle-bone-teaching/releases/download/MINI/HUST-OBC-Mini.zip
!unzip -q HUST-OBC-Mini.zip -d /content/oracle_bone/data/

# 下载模型
!wget https://github.com/zhaoyanghao125-sudo/oracle-bone-teaching/releases/download/model/max_val_acc.pth -P /content/oracle_bone/models/
```

### 加载标签映射
```python
import json

with open('HUST-OBC-Mini/deciphered/ID_to_chinese.json', 'r', encoding='utf-8') as f:
    id_to_chinese = json.load(f)

# 示例：查看ID为"1"的字符对应的现代汉字
print(id_to_chinese["1"])
```

### 加载图片
```python
from PIL import Image
import os

# 加载某个类别的图片
class_id = "1"
class_dir = f"HUST-OBC-Mini/deciphered/{class_id}"
images = [f for f in os.listdir(class_dir) if f.endswith('.png')]

img = Image.open(os.path.join(class_dir, images[0]))
img.show()
```

## 包含的字符示例

子、祝、福、牢、羌、祼、伐、逐、河、襄、鬼、酉、商、召、黍、喪、牧、自、雉、夒 ...

## 什么是甲骨文？

甲骨文是中国最早的成熟文字系统，刻写于龟甲和兽骨上，距今约3000年（商朝晚期）。1899年在河南安阳殷墟发现，至今已出土约15万片，包含4500余个单字，其中约1500个已被解读。

## 引用

如使用本数据集，请引用原作者论文：
```bibtex
@article{wang2024hust,
  title={An open dataset for oracle bone script recognition and decipherment},
  author={Wang, Pengjie and Zhang, Kaile and Wang, Xinyu and Han, Shengwei and Liu, Yongge and Wan, Jinpeng and Guan, Haisu and Kuang, Zhebin and Jin, Lianwen and Bai, Xiang and Liu, Yuliang},
  journal={Scientific Data},
  volume={11},
  number={1},
  pages={1010},
  year={2024},
  publisher={Nature Publishing Group}
}
```

## 相关资源

- [HUST-OBC 完整数据集](https://figshare.com/s/8a9c0420312d94fc01e3) - 包含1588类已解读字符和9411类未解读字符
- [HUST-OBC 官方代码](https://github.com/Pengjie-W/HUST-OBC) - 包含识别模型代码
- [Open-Oracle 项目](https://github.com/Yuliang-Liu/Open-Oracle) - 甲骨文AI研究合集

## 许可协议

本精简版数据集和模型仅供教学使用。原始数据集和模型版权归华中科技大学VLRLab所有。
