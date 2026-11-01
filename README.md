# Training a CNN from Scratch on CIFAR-10

A deep learning lab solution demonstrating how to build, train, and iteratively improve Convolutional Neural Networks (CNNs) on the [CIFAR-10](https://www.cs.toronto.edu/~kriz/cifar.html) dataset using **TensorFlow / Keras** — without any pre-trained weights.

---

## 📋 Overview

This project was completed as part of a Deep Learning lab assignment. It covers two progressive CNN architectures trained end-to-end on CIFAR-10:

| Model | Architecture | Val Accuracy (5 epochs) |
|-------|-------------|------------------------|
| **Basic CNN** | 4× Conv2D + 2× MaxPool + Dense | ~63.4% |
| **Improved CNN** | 4× Conv2D + BatchNorm + Dropout + Dense(128) | ~71.2% |

---

## 🗂️ Repository Structure

```
training-cnn-from-scratch/
├── main.ipynb          # Jupyter notebook with full implementation & outputs
├── report.pdf          # Lab report with analysis and discussion
└── README.md
```

---

## 🧠 Models

### Model 1 — Basic CNN

A straightforward sequential CNN to establish a baseline:

```
Input (32×32×3)
→ Conv2D(16, 3×3, valid) → ReLU
→ Conv2D(16, 3×3, valid) → ReLU
→ MaxPooling2D(2×2)
→ Conv2D(32, 3×3, valid) → ReLU
→ Conv2D(32, 3×3, valid) → ReLU
→ MaxPooling2D(2×2)
→ Flatten → Dense(10, softmax)
```

- **Total params:** 24,666
- **Val accuracy after 5 epochs:** ~63.4%

### Model 2 — Improved CNN

An enhanced architecture addressing overfitting and training stability:

```
Input (32×32×3)
→ [Conv2D(32, same) → BatchNorm] × 2 → MaxPool → Dropout(0.25)
→ [Conv2D(64, same) → BatchNorm] × 2 → MaxPool → Dropout(0.35)
→ Flatten → Dense(128) → BatchNorm → Dropout(0.5)
→ Dense(10, softmax)
```

Key improvements over the basic model:
- **`same` padding** — preserves spatial resolution before pooling
- **BatchNormalization** — stabilizes and accelerates training
- **Dropout (0.25 / 0.35 / 0.5)** — reduces overfitting
- **Wider filters & hidden Dense layer** — increases representational capacity
- **Val accuracy after 5 epochs:** ~71.2% (+7.8 pp over baseline)

---

## 🚀 Getting Started

### Prerequisites

- Python 3.9+
- Jupyter Notebook or [Google Colab](https://colab.research.google.com/)

### Installation

```bash
pip install tensorflow
```

> The CIFAR-10 dataset (~170 MB) is downloaded automatically by Keras on first run.

### Running the Notebook

```bash
jupyter notebook main.ipynb
```

Or open `main.ipynb` directly in [Google Colab](https://colab.research.google.com/).

---

## 📊 Dataset

**CIFAR-10** — 60,000 color images (32×32 px) across 10 classes:

`airplane · automobile · bird · cat · deer · dog · frog · horse · ship · truck`

| Split | Samples |
|-------|---------|
| Train | 50,000  |
| Test  | 10,000  |

**Preprocessing applied:**
- Pixel normalization to [0, 1]
- Data augmentation: horizontal flip, width/height shift (±10%)

---

## ⚙️ Training Configuration

| Hyperparameter | Value |
|---------------|-------|
| Optimizer | Adam |
| Loss | Categorical Cross-Entropy |
| Epochs | 5 |
| Batch size | 64 |
| Augmentation | Width/height shift ±10%, horizontal flip |

---

## 📄 Report

See [`report.pdf`](report.pdf) for the full written analysis, including architecture justification, results discussion, and conclusions.

---

## 🛠️ Tech Stack

![Python](https://img.shields.io/badge/Python-3.9%2B-blue?logo=python)
![TensorFlow](https://img.shields.io/badge/TensorFlow-2.19-orange?logo=tensorflow)
![Keras](https://img.shields.io/badge/Keras-3.13-red?logo=keras)
![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-f37626?logo=jupyter)

