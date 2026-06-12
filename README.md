# Continuous User Authentication from Mouse Dynamics using Recurrence Plot Vision Transformers

# Mouse Dynamics Intrusion Detection using Vision Transformers

## Overview

Traditional authentication systems verify users only at login, leaving systems vulnerable if an attacker gains access after authentication.

This project implements a **continuous authentication system** that identifies users based on their unique mouse movement behavior. The system transforms raw mouse trajectories into image representations using **Asymmetric Recurrence Plots (ARP)** and classifies them using a lightweight **Vision Transformer (ViT)** with **Efficient Attention** and **Gradient Harmonizing Mechanism (GHM) Loss**.

The implementation is based on the 2025 IEEE Transactions on Information Forensics and Security (TIFS) research paper:

> *A Mouse Dynamics Authentication System With a Recurrence Plot Image Representation and a Vision Transformer Framework*

---

## Problem Statement

Passwords, OTPs, and even biometric authentication verify a user only once.

What happens if an unauthorized user gains access after login?

This project addresses that challenge through **continuous behavioral authentication**, where the system continuously monitors mouse movement patterns and detects potential intruders in real time.

---

## Key Features

* Behavioral biometric authentication using mouse dynamics
* Asymmetric Recurrence Plot (ARP) generation
* Lightweight Vision Transformer architecture
* Efficient Multi-Head Attention mechanism
* Gradient Harmonizing Mechanism (GHM) loss for class imbalance
* Memory-efficient on-the-fly image generation
* User-specific intrusion detection models
* Evaluation using AUC and Equal Error Rate (EER)

---

## System Architecture

```text
Mouse Events
      │
      ▼
Coordinate Segmentation
      │
      ▼
Distance Matrix
      │
      ▼
Asymmetric Recurrence Plot (ARP)
      │
      ▼
Vision Transformer
      │
      ├── Efficient Attention
      ├── Layer Normalization
      ├── MLP Blocks
      └── Global Feature Aggregation
      │
      ▼
Intruder / Genuine User Prediction
```

---

## Technical Contributions

### 1. Asymmetric Recurrence Plot Generation

Raw mouse coordinates are converted into image representations that preserve recurrence patterns within user behavior.

Benefits:

* Captures behavioral signatures
* Reduces redundancy
* Improves transformer learning efficiency
* Produces compact 300×300 representations

---

### 2. Efficient Vision Transformer

Implemented a lightweight transformer architecture with:

* 3 Transformer Encoder Blocks
* 3 Attention Heads
* Efficient Attention mechanism
* 225-dimensional patch embeddings

Unlike traditional ViTs, this architecture is optimized for recurrence plot representations.

---

### 3. Gradient Harmonizing Mechanism (GHM)

To address severe class imbalance between genuine and impostor samples, GHM loss dynamically adjusts sample weights based on gradient density.

Benefits:

* Focuses training on hard samples
* Improves learning stability
* Better handling of minority classes

---

### 4. Memory Optimization

One of the biggest engineering challenges was storage.

#### Traditional Approach

Pre-generating all recurrence plot images:

```text
≈ 202 GB Storage Required
```

#### Implemented Solution

Custom LazyRecurrencePlotDataset:

```text
≈ 2.7 GB Memory Usage
```

### Result

```text
~75× Reduction in Memory Consumption
```

This allows large-scale training on limited hardware.

---

## Dataset

### DFL Mouse Dynamics Dataset

* 21 Users
* 499,398 Training Segments
* 62,414 Testing Segments

Mouse events contain:

* Timestamp
* X Coordinate
* Y Coordinate
* Mouse State Information

---

## Model Configuration

| Parameter           | Value   |
| ------------------- | ------- |
| Segment Length      | 600     |
| Image Size          | 300×300 |
| Patch Size          | 15×15   |
| Embedding Dimension | 225     |
| Attention Heads     | 3       |
| Transformer Layers  | 3       |
| MLP Hidden Size     | 512     |
| Batch Size          | 64      |
| Learning Rate       | 0.001   |

---

## Results

### Average Performance

| Metric          | Score  |
| --------------- | ------ |
| Mean AUC        | 0.7800 |
| Mean EER        | 0.2756 |
| Users Evaluated | 21     |

### Best Performing Users

| User   | AUC    | EER    |
| ------ | ------ | ------ |
| User4  | 0.9391 | 0.1173 |
| User17 | 0.9169 | 0.1494 |
| User9  | 0.9093 | 0.1558 |

---

## Comparison with Research Paper

| Metric       | This Work | IEEE Paper |
| ------------ | --------- | ---------- |
| Mean AUC     | 0.7800    | 0.9919     |
| Mean EER     | 0.2756    | 0.0220     |
| Dataset      | DFL       | DFL        |
| Architecture | ViT + GHM | ViT + GHM  |

### Analysis

The architectural implementation faithfully reproduces the proposed framework.

Performance differences are primarily due to:

* CPU-only training
* Single training epoch
* Limited computational resources

The original work was trained on NVIDIA Tesla V100 GPUs for significantly longer training durations.

---

## Tech Stack

### Machine Learning

* PyTorch
* Vision Transformers
* Efficient Attention
* GHM Loss

### Data Processing

* NumPy
* Pandas
* OpenCV

### Visualization

* Matplotlib
* Recurrence Plot Generation

### Domain

* Cybersecurity
* Behavioral Biometrics
* Intrusion Detection
* Continuous Authentication

---

## Future Work

* Train on GPU for full convergence
* Real-time authentication pipeline
* Streamlit/Web deployment
* Multi-modal authentication using mouse + keystroke dynamics
* Explainable AI for behavioral biometrics
* Enterprise-scale insider threat detection

---

## Why This Project Matters

This project sits at the intersection of:

* Artificial Intelligence
* Cybersecurity
* Behavioral Biometrics
* Deep Learning Research

It demonstrates the ability to:

* Read and reproduce research papers
* Implement transformer architectures from scratch
* Optimize large-scale data pipelines
* Work with real-world security datasets
* Evaluate systems using industry-standard metrics

---

## Author

**Siddhi Jadhav**

B.Tech Computer Engineering
National Institute of Technology Kurukshetra

Interested in:
Machine Learning • AI Research • Cybersecurity • Deep Learning Systems

---

⭐ If you found this project interesting, consider starring the repository.

NIT Kurukshetra
