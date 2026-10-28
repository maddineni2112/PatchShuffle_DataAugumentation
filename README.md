# PatchShuffle Data Augmentation for CIFAR-10

![Python](https://img.shields.io/badge/Python-3.x-3776AB?logo=python&logoColor=white)
![PyTorch](https://img.shields.io/badge/PyTorch-2.x-EE4C2C?logo=pytorch&logoColor=white)
![Dataset](https://img.shields.io/badge/Dataset-CIFAR--10-2F855A)
![Notebook](https://img.shields.io/badge/Format-Jupyter%20Notebook-F37626?logo=jupyter&logoColor=white)

An experimental study of **PatchShuffle**, a localized image augmentation method for convolutional neural networks. The project compares a baseline training pipeline with a pipeline that combines PatchShuffle and conventional image augmentations on CIFAR-10.

## Overview

PatchShuffle divides an image into non-overlapping patches and randomly permutes the pixels within each patch with a configurable probability. The goal is to perturb local texture while preserving the broader spatial structure of the image.

The notebook evaluates a compact CNN under two settings:

1. **Baseline:** tensor conversion and CIFAR-10 normalization.
2. **Augmented:** random crop, horizontal flip, color jitter, PatchShuffle, random erasing, and normalization.

The experiment is designed for GPU execution in Google Colab, but it also supports CPU fallback through PyTorch device detection.

## Experimental configuration

| Setting | Value |
| --- | --- |
| Dataset | CIFAR-10 |
| Model | Three-block CNN with batch normalization and dropout |
| Patch size | `4 × 4` pixels |
| PatchShuffle probability | `0.3` |
| Batch size | `128` |
| Learning rate | `0.001` |
| Epochs | `100` |
| Random seed | `42` |
| Optimizer / loss | Adam / cross-entropy |

The notebook records the comparison outputs and training curves. No accuracy or loss values are reproduced here beyond the figures and report included in this repository.

## Repository contents

| File | Description |
| --- | --- |
| [`Data_Augmentation_CodeFile.ipynb`](Data_Augmentation_CodeFile.ipynb) | End-to-end implementation, training, evaluation, and plots |
| [`DATA_AUGUMENTATION_PROJECT_REPORT.pdf`](DATA_AUGUMENTATION_PROJECT_REPORT.pdf) | Project report and methodology discussion |
| [`Data_Augmentation_PRESNTATION.pptx`](Data_Augmentation_PRESNTATION.pptx) | Presentation of the experiment |
| [`accuracy.png`](accuracy.png) | Accuracy comparison figure |
| [`loss.png`](loss.png) | Loss comparison figure |
| [`requirements.txt`](requirements.txt) | Python dependencies |
| [`CONTRIBUTING.md`](CONTRIBUTING.md) | Contribution and reproducibility guidance |

## Quick start

### 1. Create an environment

```bash
python -m venv .venv
```

Activate it on Windows:

```powershell
.\.venv\Scripts\Activate.ps1
```

Activate it on macOS/Linux:

```bash
source .venv/bin/activate
```

### 2. Install dependencies

```bash
pip install -r requirements.txt
```

### 3. Run the notebook

```bash
jupyter notebook Data_Augmentation_CodeFile.ipynb
```

The notebook downloads CIFAR-10 through `torchvision` when the dataset is not present.

## Method details

The custom transform converts a tensor from `(C, H, W)` to `(H, W, C)`, applies pixel shuffling inside each valid patch, and converts the result back to a PyTorch tensor. Border pixels are left unchanged when an image dimension is not divisible by the selected patch size.

The comparison uses the same CNN architecture and training settings for the baseline and augmented pipelines so that the augmentation strategy is the primary experimental difference.

## Reproducibility notes

- Set the random seed before training for repeatable splits and augmentation behavior.
- A CUDA device is used automatically when available; otherwise the notebook falls back to CPU.
- Training for 100 epochs can be time-consuming on CPU.
- The complete CIFAR-10 dataset is obtained at runtime from `torchvision` and is not redistributed here.

## Limitations

- Results depend on the hardware, PyTorch/torchvision versions, and runtime duration.
- PatchShuffle currently operates on non-overlapping patches and ignores non-divisible border regions.
- The repository is an experimental comparison rather than a production augmentation library.
