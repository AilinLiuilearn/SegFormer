```markdown
# Superpixel Segmentation With Edge Guided Local-Global Attention Network

> **Official PyTorch implementation of the TCSVT paper "Superpixel Segmentation With Edge Guided Local-Global Attention Network".**

## Authors

**Mingzhu Xu**<sup>1</sup>, **Zhengyu Sun**<sup>1</sup>, **Yijun Hu**<sup>1</sup>, **Haoyu Tang**<sup>1</sup>, **Yupeng Hu**<sup>1</sup>, **Xuemeng Song**<sup>2</sup>, **Liqiang Nie**<sup>2</sup>

<sup>1</sup> `Affiliation 1`  
<sup>2</sup> `Affiliation 2`  
\* Corresponding author

## Links

- **Paper**: [`IEEE Xplore`](https://doi.org/10.1109/TCSVT.2025.3587485)
- **Code Repository**: [`GitHub`](https://github.com/iLearn-Lab/ELGANet)

---

## Table of Contents

- [Updates](#updates)
- [Introduction](#introduction)
- [Highlights](#highlights)
- [Project Structure](#project-structure)
- [Installation](#installation)
- [Data Preparation](#data-preparation)
- [Usage](#usage)
- [Evaluation](#evaluation)
- [Demo / Visualization](#demo--visualization)
- [Citation](#citation)
- [License](#license)

---

## Updates

- [04/2026] Initial release of the official implementation.
- [01/2025] Paper published in IEEE TCSVT.

---

## Introduction

本项目是论文 **"Superpixel Segmentation With Edge Guided Local-Global Attention Network" (ELGANet)** 的官方实现。

超像素分割是计算机视觉中的基础任务。ELGANet 通过引入边缘引导（Edge-Guided）机制与本地-全局注意力网络（Local-Global Attention），显著提升了分割边缘的拟合精度与语义一致性。

本仓库提供了：
- 完整的训练与推理代码。
- 边缘引导的局部-全局注意力网络模型实现。
- 基于 BSDS500 数据集的预处理与评测全流程脚本。

---

## Highlights

- **Edge-Guided Attention**: 利用边缘信息精细化超像素边界。
- **Local-Global Context**: 同时捕捉局部细节与全局上下文信息。
- **High Efficiency**: 优化的 PyTorch 实现，结合 Cython 后处理确保连通性。
- **State-of-the-art Performance**: 在 ASA, CO 和 BR-BP 指标上表现优异。

---

## Project Structure

```text
.
├── data_preprocessing/    # BSDS500 数据处理脚本
├── eval_spixel/           # 评测脚本 (bash & MATLAB)
├── third_party/           # 外部依赖 (含 Cython 连通性插件)
├── main.py                # 训练主程序
├── run_demo.py            # 推理 Demo
├── requirements.txt       # 环境依赖
└── LICENSE                # 项目授权协议
```

---

## Installation

### 1. Clone the repository

```bash
git clone [https://github.com/iLearn-Lab/ELGANet.git](https://github.com/iLearn-Lab/ELGANet.git)
cd ELGANet
```

### 2. Prerequisites & Cython Compilation
为了确保超像素的连通性（connectivity），需要编译 `third_party` 中的组件：

```bash
cd third_party/cython/
python setup.py install --user
cd ../..
```

### 3. Install dependencies
```bash
pip install -r requirements.txt
```

---

## Data Preparation 

1. 从 [BSDS500](http://www.eecs.berkeley.edu/Research/Projects/CS/vision/grouping/BSR/BSR_full.tgz) 下载原始数据并解压至 `<BSDS_DIR>`。
2. 运行预处理脚本生成训练与测试集：

```bash
cd data_preprocessing
python pre_process_bsd500.py --dataset=<BSDS_DIR> --dump_root=<DUMP_DIR>
python pre_process_bsd500_ori_sz.py --dataset=<BSDS_DIR> --dump_root=<DUMP_DIR>
cd ..
```
生成的目录结构包含 `/train`, `/val`, `/test` 文件夹及对应的路径记录 `.txt` 文件。

---

## Usage

### Training
使用准备好的数据开始训练：
```bash
python main.py --data=<DUMP_DIR> --savepath=<CKPT_LOG_DIR>
```

使用预训练模型进行微调或恢复训练：
```bash
python main.py --data=<DUMP_DIR> --savepath=<CKPT_LOG_DIR> --pretrained=<PATH_TO_THE_CKPT> 
```

### Demo
对特定目录下的图像生成超像素可视化结果：
```bash
python run_demo.py --data_dir=PATH_TO_IMAGE_DIR --output=./demo 
```
结果将生成在 `./demo/spixel_viz` 目录下。

---

## Evaluation

遵循 [FCN](https://github.com/fuy34/superpixel_fcn) 的评测流程，使用 [superpixel benchmark](https://github.com/davidstutz/superpixel-benchmark) 进行评估。

1. 下载并根据 [说明](https://github.com/davidstutz/superpixel-benchmark/blob/master/docs/BUILDING.md) 编译评测代码。
2. 编辑 `eval_spixel/my_eval.sh` 中的变量（如 `IMG_PATH`, `GT_PATH`, `SEG_PATH`）。
3. 运行评测 Shell：
   ```bash
   cp eval_spixel/my_eval.sh <path/to/benchmark>/examples/bash/
   cd <path/to/benchmark>/examples/
   bash my_eval.sh
   ```
4. 在 MATLAB 中配置 `plot_benchmark_curve.m` 中的路径并运行，即可查看 **ASA**, **CO**, 和 **BR-BP** 曲线。

---

## Citation

如果您在研究中使用了本代码或方法，请引用我们的工作：

```bibtex
@ARTICLE{ELGANet,
  author={Xu, Mingzhu and Sun, Zhengyu and Hu, Yijun and Tang, Haoyu and Hu, Yupeng and Song, Xuemeng and Nie, Liqiang},
  journal={IEEE Transactions on Circuits and Systems for Video Technology}, 
  title={Superpixel Segmentation With Edge Guided Local-Global Attention Network}, 
  year={2025},
  volume={},
  number={},
  pages={1-1},
  keywords={Image edge detection;Feature extraction;Convolution;Training;Semantics;Object detection;Circuits and systems;Visualization;Data mining;Iterative methods;Superpixel segmentation;Edge enhancement;Local-Global context},
  doi={10.1109/TCSVT.2025.3587485}
}
```

---

## Acknowledgement

- 感谢 [SSN](https://github.com/NVlabs/ssn_superpixels) 提供的组件连接代码。
- 感谢 [superpixel-benchmark](https://github.com/davidstutz/superpixel-benchmark) 提供的标准评测工具。

---

## License

This project is released under the Apache License 2.0.
```
