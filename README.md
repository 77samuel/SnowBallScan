
# SnowBallScan

**Measuring Sequential Hallucination Propagation and Self-Correction in Small Language Models**

[![Paper](https://img.shields.io/badge/Paper-Applied%20Intelligence-blue)](https://link.springer.com/journal/10489)
[![License](https://img.shields.io/badge/License-MIT-green)](LICENSE)

## Overview

SnowBallScan is an evaluation framework for measuring how hallucinations evolve across sequential generation chains in small language models (SLMs). It introduces two metrics:

- **PAI (Propagation Amplification Index)** — ratio of hallucination rate at step k to baseline step 1
- **Snowball Onset Step** — earliest chain position where PAI exceeds a risk threshold (θ=1.5)

## Key Findings

- Small LMs exhibit **domain-dependent** sequential behaviour
- On seeded hallucination inputs (HaluEval), all models **self-correct** strongly (PAI drops to 0.48)
- On factual/temporal domains, mild propagation observed (PAI up to 1.17 at K=5)
- At K=10, TinyLlama on TruthfulQA **first reaches onset at step 2** (PAI=1.545)
- A neutral-context ablation confirms self-correction is **context-driven**, not prompt-induced
- Lightweight training-free mitigation reduces step-5 hallucination rates by up to **42.5%**

## Models Evaluated

| Model | Parameters |
|-------|-----------|
| Phi-2 | 2.7B |
| TinyLlama | 1.1B |
| Qwen 2.5 | 1.5B |

## Datasets

| Dataset | Domain | N |
|---------|--------|---|
| TruthfulQA | General Factual | 200 |
| FreshQA | Temporal | 200 |
| HaluEval QA | Multi-domain | 200 |

## Repository Structure

```
snowballscan_main.py     # Main experiment (n=200, K=5, FP16)
snowballscan_extra.py    # Extended experiments (neutral context + K=10)
requirements.txt         # Dependencies
```

## Setup

```bash
pip install -r requirements.txt
```

## Usage

### Main Experiment (K=5, n=200, all datasets)

```bash
python snowballscan_main.py
```

### Extended Experiments

```python
# In snowballscan_extra.py, set RUN_MODE at the top:

RUN_MODE = "neutral"   # Neutral context ablation (HaluEval, n=200, K=5)
RUN_MODE = "k10"       # Extended chains (all datasets, n=100, K=10)
```

## Results

Experimental results are archived on Zenodo:

- Main experiment: `snowballscan_results_v10.xlsx`
- Neutral context ablation: `results_neutral.xlsx`
- K=10 extended chains: `results_k10.xlsx`

## Citation

Citation will be added upon publication.


## Authors

- **Samuel Stephen** — Karunya Institute of Technology and Sciences
  - ORCID: 0009-0002-9446-000X
  - Email: samuels24@karunya.edu.in
- **R. Vignesh** — Karunya Institute of Technology and Sciences
  - ORCID: 0009-0008-0134-8726

## License

MIT License
