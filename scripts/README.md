# scripts/

本文件夹存放**训练、评测、数据预处理**相关的运行脚本。

## 文件说明

| 脚本 | 功能 |
|---|---|
| `preprocess.py` | 数据预处理 |
| `train.sh` | 启动训练 |
| `eval.sh` | 启动评测 |

> 根据你的实际情况增删上表中的条目。

## 训练

```bash
bash scripts/train.sh \
    --model 【模型名】 \
    --data_dir ./data/processed \
    --output_dir ./results
```

主要参数说明：

| 参数 | 默认值 | 说明 |
|---|---|---|
| `--model` | 【默认值】 | 使用的基础模型 |
| `--data_dir` | `./data/processed` | 数据路径 |
| `--output_dir` | `./results` | 输出路径 |

## 评测

```bash
bash scripts/eval.sh \
    --model 【模型名】 \
    --benchmark 【benchmark名称】
```

支持的 benchmark：

- 【benchmark 1】
- 【benchmark 2】
