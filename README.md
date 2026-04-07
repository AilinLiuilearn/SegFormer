# HDNet: A Hybrid Domain Network with Multi-Scale High-Frequency Information Enhancement for Infrared Small Target Detection

> **Official PyTorch implementation of the TGRS 2025 paper "HDNet: A Hybrid Domain Network with Multi-Scale High-Frequency Information Enhancement for Infrared Small Target Detection".**

## Authors

**Mingzhu Xu**<sup>1</sup>, **Chenglong Yu**<sup>1</sup>, **Zexuan Li**<sup>1</sup>, **Haoyu Tang**<sup>1</sup>, **Yupeng Hu**<sup>1</sup>, **Liqiang Nie**<sup>1</sup>\*

<sup>1</sup> `Shandong University`  
\* Corresponding author

## Links

- **Paper**: [`IEEE Xplore`](https://ieeexplore.ieee.org/document/11017756)
- **Code Repository**: [`GitHub`](https://github.com/iLearn-Lab/HDNet)

---

## Table of Contents

- [Updates](#updates)
- [Introduction](#introduction)
- [Highlights](#highlights)
- [Method / Framework](#method--framework)
- [Project Structure](#project-structure)
- [Installation](#installation)
- [Dataset](#dataset)
- [Usage](#usage)
- [Quantitative Results](#quantitative-results)
- [Citation](#citation)
- [Acknowledgement](#acknowledgement)
- [License](#license)

---

## Updates

- [03/2026] Initial release of HDNet training and testing codes.
- [01/2025] Paper published in IEEE TGRS.

---

## Introduction

本项目是论文 **"HDNet: A Hybrid Domain Network with Multi-Scale High-Frequency Information Enhancement for Infrared Small Target Detection"** 的官方实现。

HDNet 提出了一种创新的混合域网络，通过融合频域特征与传统的空域 CNN 特征，显著增强了红外弱小目标的对比度并抑制背景干扰：
- **空域分支**：引入 **多尺度空洞对比卷积 (MAC)** 模块，增强对不同尺寸弱小目标的感知能力。
- **频域分支**：设计 **动态高通滤波器 (DHPF)** 模块，动态移除低频背景干扰，保留高频目标细节。
- **实验表现**：在 IRSTD-1K, NUAA-SIRST, NUDT-SIRST 三大数据集上超越了 26 种 SOTA 方法。

### Example Description

We present **HDNet**, a framework for **Infrared Small Target Detection (IRSTD)**.  
Our method addresses **background interference and low contrast** by introducing **hybrid domain feature fusion** and **dynamic high-pass filtering**.  
This repository provides the official implementation, pretrained weights, and evaluation scripts.

---

## Highlights

- 提出 **Hybrid-Domain Network (HDNet)**，结合空域多尺度感知与频域背景抑制。
- 创新性 **MAC 模块**，提升小目标与复杂背景的对比度。
- 创新性 **DHPF 模块**，动态抑制缓慢变化的低频背景噪声。
- 提供在三大公开数据集上的完整评估结果。

---

## Method / Framework

HDNet 架构图展示了空域与频域双分支协作流程。

### Framework Figure

![Framework](./Fig/Structure.png)

**Figure 1.** Overall framework of HDNet.

---

## Project Structure

```text
.
├── Fig/                   # 架构图及可视化结果
├── datasets/              # 存放数据集 (IRSTD-1k, NUAA-SIRST, NUDT-SIRST)
├── weight/                # 存放预训练权重 (.pkl)
├── main.py                # 主程序入口
├── README.md
└── requirements.txt
````

-----

## Installation

### 1\. Clone the repository

```bash
git clone [https://github.com/iLearn-Lab/HDNet.git](https://github.com/iLearn-Lab/HDNet.git)
cd HDNet
```

### 2\. Prerequisites

本项目在 Ubuntu 22.04 环境下开发，推荐配置如下：

  - Python 3.10
  - PyTorch 2.1.0
  - CUDA 12.1

<!-- end list -->

```bash
pip install -r requirements.txt
```

-----

## Dataset

请下载以下数据集并放入 `./datasets` 目录：

  - [IRSTD-1k](https://github.com/RuiZhang97/ISNet)
  - [NUAA-SIRST](https://github.com/YimianDai/sirst)
  - [NUDT-SIRST](https://github.com/YeRen123455/Infrared-Small-Target-Detection)

-----

## Usage

### Training

```bash
python main.py --dataset-dir './dataset/IRSTD-1k' --batch-size 4 --epochs 800 --mode 'train'
```

### Testing

```bash
python main.py --dataset-dir './dataset/IRSTD-1k' --batch-size 4 --mode 'test' --weight-path './weight/irstd.pkl'
```

-----

## Quantitative Results

| Dataset | mIoU (x10⁻²) | Pd (x10⁻²) | Fa (x10⁻⁶) | Weights |
| :--- | :---: | :---: | :---: | :---: |
| IRSTD-1k | 70.26 | 94.56 | 4.33 | [Download](https://drive.google.com/file/d/1WjKkkfIRlI7aNlu4xTglmVxwtDqlu4Gu/view?usp=drive_link) |
| NUAA-SIRST | 79.17 | 100 | 0.53 | [Download](https://drive.google.com/file/d/1GoCaiAEodUop5EPyDWu5LEfJ71D1kOz2/view?usp=drive_link) |
| NUDT-SIRST | 85.17 | 98.52 | 2.78 | [Download](https://drive.google.com/file/d/1we0dE2L47z509-EW4_Bj4Y828oPSkNAe/view?usp=drive_link) |

可视化结果请参考：[HDNet\_Visual\_Result](https://www.google.com/search?q=https://drive.google.drive/folders/1RfoxhoHpjfbRMZHBOvISrJSB5lpoz40t%3Fusp%3Ddrive_link)

-----

## Citation

如果您在研究中使用了本代码，请引用我们的论文：

```bibtex
@ARTICLE{11017756,
  author={Xu, Mingzhu and Yu, Chenglong and Li, Zexuan and Tang, Haoyu and Hu, Yupeng and Nie, Liqiang},
  journal={IEEE Transactions on Geoscience and Remote Sensing}, 
  title={HDNet: A Hybrid Domain Network With Multiscale High-Frequency Information Enhancement for Infrared Small-Target Detection}, 
  year={2025},
  volume={63},
  number={},
  pages={1-15},
  doi={10.1109/TGRS.2025.3574962}
}
```

-----

## Acknowledgement

  - HDNet 采用了 SLS 损失函数，并基于 [MSHNet](https://github.com/Lliu666/MSHNet) 进行了架构改进。特别感谢 Qiankun Liu 的工作。

-----

## License

This project is released under the Apache License 2.0.
