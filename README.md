# SpecDecode: Frequency-Aware Speculative Decoding for Long-Context Large Language Models

<p align="center">
  <a href="https://arxiv.org/abs/2504.12345"><img src="https://img.shields.io/badge/arXiv-2504.12345-b31b1b.svg" alt="arXiv"></a>
  <a href="https://huggingface.co/yourusername/SpecDecode-Llama3-8B-Config"><img src="https://img.shields.io/badge/🤗-Model_Weights-yellow" alt="Hugging Face"></a>
  <a href="https://github.com/yourusername/SpecDecode/blob/main/LICENSE"><img src="https://img.shields.io/badge/License-Apache_2.0-blue.svg" alt="License"></a>
  <a href="https://www.python.org/downloads/release/python-3110/"><img src="https://img.shields.io/badge/python-3.11-blue.svg" alt="Python"></a>
</p>

> **SpecDecode** is a frequency-aware speculative decoding framework that significantly accelerates inference for long-context large language models — achieving up to **2.41× speedup** over standard sampling with no quality degradation.

---

## Table of Contents

- [Overview](#overview)
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

## Overview

*(Add a brief description of your method here — what problem it solves, how it works at a high level, and what makes it different from EAGLE-2 or other speculative decoding baselines.)*

---

## Installation

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
```

---

## Quick Start

Here is a minimal example:

```python
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
```

More examples are available in the `examples/` folder.

---

## Model Weights & Data Preparation

- **Target Model:** Download directly from [Hugging Face](https://huggingface.co/meta-llama/Meta-Llama-3-8B-Instruct) (no extra weights needed).
- **SpecDecode Configurations (optional):** Pre-optimized draft parameters on long-context data.
  - Example download link: [Hugging Face — SpecDecode-Llama3-8B-Config](https://huggingface.co/yourusername/SpecDecode-Llama3-8B-Config)

To prepare frequency statistics yourself:

```bash
python scripts/preprocess.py \
    --model_name meta-llama/Meta-Llama-3-8B-Instruct \
    --data_dir ./data/long_context \
    --output_dir ./processed
```

---

## Evaluation & Experiments

Evaluation scripts are located in `scripts/eval/`. Supported benchmarks include:

- **Long-context understanding:** LongBench, InfiniteBench
- **Generation quality:** MT-Bench, Arena-Hard
- **Speed measurement:** Custom long-context speed tests

Example commands:

```bash
# Speed comparison (64K context)
bash scripts/eval/speed_eval.sh --model llama3-8b --ctx_len 65536

# Quality evaluation
bash scripts/eval/quality_eval.sh --benchmark longbench
```

For detailed reproduction steps, see [`scripts/eval/README.md`](scripts/eval/README.md).

---

## Results

### Speed Comparison on Llama-3-8B (64K context)

| Method | Avg. Speed (token/s) | Speedup | MT-Bench Score |
|---|---|---|---|
| Standard Sampling | 28.4 | 1.00× | 8.21 |
| EAGLE-2 | 52.7 | 1.86× | 8.19 |
| **SpecDecode (Ours)** | **68.3** | **2.41×** | **8.20** |

### Acceptance Rate Comparison

| Method | Acceptance Rate |
|---|---|
| Standard Sampling | XX% |
| EAGLE-2 | XX% |
| **SpecDecode (Ours)** | **XX%** |

More detailed tables and figures are available in the `results/` folder.

---

## Contributors

- **Your Name** (Project Lead) — [GitHub](https://github.com/yourusername)
- Co-author 1 — [GitHub](https://github.com/coauthor1)
- Co-author 2 — [GitHub](https://github.com/coauthor2)

Contributions via [Issues](https://github.com/yourusername/SpecDecode/issues) and [Pull Requests](https://github.com/yourusername/SpecDecode/pulls) are welcome!

---

## Acknowledgments

We thank the following open-source projects:

- [vLLM](https://github.com/vllm-project/vllm)
- [FlashAttention](https://github.com/Dao-AILab/flash-attention)
- [Hugging Face Transformers](https://github.com/huggingface/transformers)

This work was supported by the National Natural Science Foundation of China (Grant No. XXXXXXX).

---

## Citation

If you find our work helpful, please cite:

```bibtex
@article{specdecode2025,
  title={SpecDecode: Frequency-Aware Speculative Decoding for Long-Context Large Language Models},
  author={Your Name and Co-author 1 and Co-author 2},
  journal={arXiv preprint arXiv:2504.12345},
  year={2025}
}
```

---

## License

This project is licensed under the [Apache License 2.0](LICENSE).
