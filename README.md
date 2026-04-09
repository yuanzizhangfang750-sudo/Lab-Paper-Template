# SpecDecode: Efficient Speculative Decoding for Long-Context LLMs

[![arXiv](https://img.shields.io/badge/arXiv-2504.12345-b31b1b.svg)](https://arxiv.org/abs/2504.12345)
[![License](https://img.shields.io/badge/License-Apache_2.0-blue.svg)](LICENSE)
[![Python](https://img.shields.io/badge/Python-3.10%2B-blue)](https://www.python.org/)
[![PyTorch](https://img.shields.io/badge/PyTorch-2.3%2B-orange)](https://pytorch.org/)

> **SpecDecode** is the official implementation of the paper "SpecDecode: Frequency-Aware Speculative Decoding for Long-Context Large Language Models". It achieves up to **2.4×** decoding speedup on 64K+ context lengths while maintaining generation quality, without any retraining of the target model.

## Table of Contents

- [Introduction](#introduction)
- [News & Updates](#news--updates)
- [Key Features](#key-features)
- [Installation](#installation)
- [Quick Start](#quick-start)
- [Model Weights & Data Preparation](#model-weights--data-preparation)
- [Evaluation & Experiments](#evaluation--experiments)
- [Results](#results)
- [Contributors](#contributors)
- [Acknowledgments](#acknowledgments)
- [Citation](#citation)
- [License](#license)

---

## Introduction

As the context window of large language models continues to expand to 128K tokens and beyond, the autoregressive decoding bottleneck becomes increasingly severe. Existing speculative decoding methods suffer from significant performance degradation in long-context scenarios due to poor draft acceptance rates.

**SpecDecode** introduces a frequency-aware dynamic drafting mechanism and position-sensitive verification strategy to effectively address this issue. This repository provides complete inference acceleration code, evaluation scripts, and experiment reproduction support for mainstream open-source LLMs such as **Llama-3** and **Qwen2**.

**Paper Link**: [arXiv](https://arxiv.org/abs/2504.12345) | [PDF](https://arxiv.org/pdf/2504.12345.pdf)

**Main Contributions**:

- Frequency-aware speculative sampling that significantly improves acceptance rates in long contexts
- Lightweight position interpolation module without modifying the target model weights
- State-of-the-art speedup on multiple long-context benchmarks while preserving output quality

---

## News & Updates

- **2026.04.09**: Project officially open-sourced (v1.0 release) with support for Llama-3 and Qwen2 models.
- **2025.12**: Paper accepted to ACL 2026.
- **2025.10**: arXiv preprint released.

---

## Key Features

- ✨ **Plug-and-Play**: No fine-tuning or modification of the target model required
- 🚀 **Long-Context Optimized**: Up to 2.4× speedup at 64K+ context lengths
- 📊 **Quality Preservation**: Strict verification ensures output quality matches standard sampling
- 🔧 **Framework Support**: Compatible with Hugging Face, vLLM, and SGLang
- ⚡ **Efficient CUDA Implementation**: Core modules accelerated with C++/CUDA

---

## Installation

### Requirements

- Python 3.10+
- CUDA 12.1+
- PyTorch 2.3+

```bash
# 1. Create conda environment (recommended)
conda create -n specdecode python=3.11
conda activate specdecode

# 2. Install PyTorch (adjust according to your CUDA version)
pip install torch torchvision torchaudio --index-url https://download.pytorch.org/whl/cu121

# 3. Clone and install SpecDecode
git clone https://github.com/yourusername/SpecDecode.git
cd SpecDecode
pip install -e .
Quick Start

Here is a minimal example:

from specdecode import SpecDecodeDraft, generate

# Load target model (Hugging Face format)
model_name = "meta-llama/Meta-Llama-3-8B-Instruct"

# Initialize SpecDecode
draft_model = SpecDecodeDraft.from_pretrained(
    model_name=model_name,
    draft_length=8,
    device="cuda"
)

# Generate output
prompt = "Explain the latest advances in quantum computing in 2026."
output = generate(
    model=draft_model,
    prompt=prompt,
    max_new_tokens=512,
    temperature=0.7,
    top_p=0.9
)

print(output)

More examples are available in the examples/ folder.

Model Weights & Data Preparation

Target Model: Download directly from Hugging Face (no extra weights needed).
SpecDecode Configurations (optional): Pre-optimized draft parameters on long-context data.

Example download link: Hugging Face - SpecDecode-Llama3-8B-Config

To prepare frequency statistics yourself:

python scripts/preprocess.py \
    --model_name meta-llama/Meta-Llama-3-8B-Instruct \
    --data_dir ./data/long_context \
    --output_dir ./processed
Evaluation & Experiments

Evaluation scripts are located in scripts/eval/. Supported benchmarks include:

Long-context understanding: LongBench, InfiniteBench
Generation quality: MT-Bench, Arena-Hard
Speed measurement: Custom long-context speed tests

Example commands:

# Speed comparison (64K context)
bash scripts/eval/speed_eval.sh --model llama3-8b --ctx_len 65536

# Quality evaluation
bash scripts/eval/quality_eval.sh --benchmark longbench

Detailed reproduction guide: scripts/eval/README.md

Results
Speed Comparison on Llama-3-8B (64K context)
Method	Avg. Speed (token/s)	Speedup	MT-Bench Score
Standard Sampling	28.4	1.00×	8.21
EAGLE-2	52.7	1.86×	8.19
SpecDecode (Ours)	68.3	2.41×	8.20

More detailed tables and figures are available in the results/ folder.

Acceptance Rate Comparison
Method	Acceptance Rate
Standard Sampling	XX%
EAGLE-2	XX%
SpecDecode (Ours)	XX%
Contributors
Your Name (Project Lead) — GitHub
Co-author 1 — GitHub
Co-author 2 — GitHub

Contributions via Issues and Pull Requests are welcome!

Acknowledgments

We thank the following open-source projects:

vLLM
FlashAttention
Hugging Face Transformers

This work was supported by the National Natural Science Foundation of China (Grant No. XXXXXXX).

Citation

If you find our work helpful, please cite:

@article{specdecode2025,
  title={SpecDecode: Frequency-Aware Speculative Decoding for Long-Context Large Language Models},
  author={Your Name and Co-author 1 and Co-author 2},
  journal={arXiv preprint arXiv:2504.12345},
  year={2025}
}
License

This project is licensed under the Apache License 2.0.
See the LICENSE file for details.
