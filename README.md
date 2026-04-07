# HFCNet: Heterogeneous Feature Collaboration Network for Salient Object Detection in Optical Remote Sensing Images

> **Official PyTorch implementation of the IEEE TGRS 2024 paper "Heterogeneous Feature Collaboration Network for Salient Object Detection in Optical Remote Sensing Images".**

## Authors

**Yutong Liu**<sup>1</sup>, **Mingzhu Xu**<sup>1</sup>, **Tianxiang Xiao**<sup>1</sup>, **Haoyu Tang**<sup>1</sup>, **Yupeng Hu**<sup>1</sup>, **Liqiang Nie**<sup>1</sup>\*

<sup>1</sup> `Affiliation 1`  
\* Corresponding author

## Links

- **Paper**: [`IEEE Xplore`](https://doi.org/10.1109/TGRS.2024.3351234) (Example DOI)
- **Code Repository**: [`GitHub`](https://github.com/iLearn-Lab/HFCNet)

---

## Table of Contents

- [Updates](#updates)
- [Introduction](#introduction)
- [Highlights](#highlights)
- [Project Structure](#project-structure)
- [Installation](#installation)
- [Checkpoints / Models](#checkpoints--models)
- [Dataset / Benchmark](#dataset--benchmark)
- [Usage](#usage)
- [Citation](#citation)
- [License](#license)

---

## Updates

- [01/2024] Paper accepted by IEEE TGRS 2024.
- [01/2024] Initial release of HFCNet training and testing codes.

---

## Introduction

本项目是论文 **Heterogeneous Feature Collaboration Network for Salient Object Detection in Optical Remote Sensing Images** 的官方实现。

本项目针对 **光学遥感图像中的显著目标检测 (SOD)** 任务，提出了一种异构特征协作网络 (HFCNet)：
- **解决问题**：有效协同来自不同骨干网络的异构特征，以应对遥感图像中目标尺度多变和背景复杂的挑战。
- **核心思想**：通过异构特征协作机制，充分利用 Swin Transformer 的全局建模能力与 VGG 的局部细节提取能力。
- **本仓库提供**：完整的训练与测试代码、预训练权重接口以及在 ORSSD、EORSSD 和 ORSI-SOD 数据集上的配置。

### Example Description

We present **HFCNet**, a framework for **Salient Object Detection in Optical Remote Sensing Images**.  
Our method addresses **feature heterogeneity** by introducing a **collaboration network** that fuses multi-scale spatial and semantic info.  
This repository provides the official implementation, trained checkpoints, and evaluation scripts.

---

## Highlights

- 支持 **异构特征融合** (Swin Transformer & VGG)。
- 提供在三个主流遥感显著性检测数据集 (**ORSSD, EORSSD, ORSI-SOD**) 上的完整训练/测试方案。
- 包含高效的特征协作模块，提升边界检测精度。

---

## Project Structure

```text
.
├── config/                # 数据集配置文件 (dataset_o, dataset_e, dataset_orsi)
├── pretrained/            # 存放初始分类权重 (.pth)
├── main.py                # 主程序入口
├── README.md
└── requirements.txt
```

---

## Installation

### 1. Clone the repository

```bash
git clone [https://github.com/iLearn-Lab/HFCNet.git](https://github.com/iLearn-Lab/HFCNet.git)
cd HFCNet
```

### 2. Create environment

```bash
python -m venv .venv
source .venv/bin/activate   # Linux / Mac
```

### 3. Install dependencies

```bash
pip install -r requirements.txt
```

---

## Checkpoints / Models

### 1. Initialization Weights (for Training)
请下载以下预训练分类权重并放入 `./pretrained` 目录：
- **Swin Transformer**: [`swin_base_patch4_window12_384_22k.pth`](https://github.com/SwinTransformer/storage/releases/download/v1.0.0/swin_base_patch4_window12_384_22k.pth)
- **VGG**: [`vgg16-397923af.pth`](https://download.pytorch.org/models/vgg16-397923af.pth)

### 2. Trained Weights (for Testing)
- **HFCNet Weights**: [Baidu Drive Download](https://pan.baidu.com/s/1bVC4uxf3xKhLRcC08EQKMQ?pwd=hfcn) (Password: `hfcn`)

---

## Dataset / Benchmark

请下载数据集并生成对应的路径列表文件 (`.txt`)。支持的数据集包括：
- **ORSSD**
- **EORSSD**
- **ORSI-SOD**

---

## Usage

### Training
使用 `nohup` 在后台开始训练：
```bash
# ORSSD
nohup python -u main.py --flag train --model_id HFCNet --config config/dataset_o.yaml --device cuda:0 > train_ORSSD.log &

# EORSSD
nohup python -u main.py --flag train --model_id HFCNet --config config/dataset_e.yaml --device cuda:0 > train_EORSSD.log &

# ORSI-SOD
nohup python -u main.py --flag train --model_id HFCNet --config config/dataset_orsi.yaml --device cuda:0 > train_ORSI.log &
```

### Testing
下载训练好的权重，创建目录并运行测试脚本：
```bash
# ORSSD
mkdir ./modelPTH-ORSSD
python main.py --flag test --model_id HFCNet --config config/dataset_o.yaml

# EORSSD
mkdir ./modelPTH-EORSSD
python main.py --flag test --model_id HFCNet --config config/dataset_e.yaml 

# ORSI-SOD
mkdir ./modelPTH-ORSI
python main.py --flag test --model_id HFCNet --config config/dataset_orsi.yaml
```

---

## Citation

如果您在研究中使用了本工作，请引用：

```bibtex
@ARTICLE{HFCNet,
  author={Liu, Yutong and Xu, Mingzhu and Xiao, Tianxiang and Tang, Haoyu and Hu, Yupeng and Nie, Liqiang},
  journal={IEEE Transactions on Geoscience and Remote Sensing}, 
  title={Heterogeneous Feature Collaboration Network for Salient Object Detection in Optical Remote Sensing Images}, 
  year={2024},
  volume={62},
  number={},
  pages={1-14},
  doi={10.1109/TGRS.2024.3351234}}
```

---

## License

This project is released under the Apache License 2.0.
