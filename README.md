# Lab-Paper-Template

[![arXiv](https://img.shields.io/badge/arXiv-XXXX.XXXXX-b31b1b.svg)](https://arxiv.org/abs/XXXX.XXXXX) 
[![License](https://img.shields.io/badge/License-MIT-blue.svg)](https://opensource.org/licenses/MIT)

## Introduction

> This is the C/CUDA implementation for [Your Method Name].

[Brief highlight of the key innovation or improvement].

[Main result, e.g. XX% / X.Xx speedup] over baseline.

Our method is simple to implement, preserves generation quality, and requires no retraining.

👉 **[Read our paper](https://arxiv.org/abs/XXXX.XXXXX)**

## Decoding Speed

<div align="center">
  <img src="assets/speed_compare.png" alt="Method Architecture" width="800px">
</div>
Decoding speed (token/s) comparison under different frameworks.

## News

**YYYY.MM.DD** [News item 1]  
**YYYY.MM.DD** [News item 2]  
...

## Installation from source

```bash
conda create -n your-project python==3.11 && conda activate your-project
# install pytorch for your platform, see https://pytorch.org
git clone https://github.com/yourusername/your-repo.git --recursive && cd your-repo
vim setup.py # change arch="80" to your GPU compute capability
pip install .
